# 通过阿里云Prometheus监控Go应用

通过在应用中埋点来暴露应用数据，使用阿里云Prometheus监控抓取数据，借助Prometheus Grafana大盘来展示数据，并创建报警，即可实现利用Prometheus监控Go应用的目的。本文以阿里云容器服务K8s集群和阿里云容器镜像服务为例，介绍如何通过Prometheus监控Go应用。

在开始本教程前，确保您已经完成了以下操作：

-   阿里云容器服务K8s集群已接入阿里云Prometheus监控。如何接入，请参见[容器服务Kubernetes版集群]()。
-   已创建阿里云容器镜像服务镜像仓库。如何创建，请参见[创建镜像仓库]()。

## Demo

如需快速体验如何通过Prometheus监控Go应用，您可以使用已埋点的[Demo工程](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo)。

## 操作流程

通过阿里云Prometheus监控Go应用的操作流程如下图所示。

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3649944261/p245640.png)

## 步骤一：为应用埋点

为应用埋点以暴露Go应用数据的操作步骤如下：

1.  将监控包导入Go应用。

    ```
    import (
        "fmt"
        "github.com/prometheus/client_golang/prometheus/promhttp"
        "net/http"
        "strconv"
    )
    ```

2.  将监控接口绑定至promhttp.Handler\(\)。

    ```
    http.Handle(path, promhttp.Handler()) //初始化一个HTTP Handler。
    ```


## 步骤二：上传应用

将完成埋点的应用制作成镜像并上传至阿里云容器镜像服务的镜像仓库的操作步骤如下：

1.  执行以下命令重新编译模块。

    ```
    mvn clean install -DskipTests
    ```

2.  执行以下命令构建镜像。

    ```
    docker build -t <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> . --no-cache
    ```

    示例命令：

    ```
    docker build -t prometheus-go-demo:v0 . --no-cache
    ```

3.  执行以下命令为镜像打标。

    ```
    sudo docker tag <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    示例命令：

    ```
    sudo docker tag prometheus-go-demo:v0 registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-go-demo:v0
    ```

4.  执行以下命令将镜像推送至镜像仓库。

    ```
    sudo docker push <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    示例命令：

    ```
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-go-demo:v0
    ```

    [容器镜像服务控制台](https://cr.console.aliyun.com)的**镜像版本**页面显示上传的应用镜像。

    ![镜像](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0962584161/p245561.png)


## 步骤三：部署应用

将应用部署至容器服务K8s集群的操作步骤如下：

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏，选择**集群**。

3.  在集群列表页面，找到目标集群，在其右侧**操作**列单击**应用管理**。

4.  创建容器组。

    1.  在左侧导航栏，选择**工作负载** \> **无状态**。

    2.  在**无状态**页面，单击**使用模板创建**。

    3.  在**创建**页面的**模板**代码框输入以下内容，然后单击**创建**。

        ```
        apiVersion: apps/v1 # for versions before 1.8.0 use apps/v1beta1
        kind: Deployment
        metadata:
          name: prometheus-go-demo
          labels:
            app: go-exporter
        spec:
          replicas: 2
          selector:
            matchLabels:
              app: go-exporter
          template:
            metadata:
              labels:
                app: go-exporter
            spec:
              containers:
              - name: prometheus-go-demo
                imagePullPolicy: Always
                image: <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
                ports:
                - containerPort: 8077
                  name: arms-go-demo
        ```

        示例代码：

        ```
        apiVersion: apps/v1 # for versions before 1.8.0 use apps/v1beta1
        kind: Deployment
        metadata:
          name: prometheus-go-demo
          labels:
            app: go-exporter
        spec:
          replicas: 2
          selector:
            matchLabels:
              app: go-exporter
          template:
            metadata:
              labels:
                app: go-exporter
            spec:
              containers:
              - name: prometheus-go-demo
                imagePullPolicy: Always
                image: registry.cn-hangzhou.aliyuncs.com/fuling/prometheus-go-demo:v0
                ports:
                - containerPort: 8077
                  name: arms-go-demo
        ```

    **无状态**页面显示创建的容器组。

    ![go-exporter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5153455161/p248949.png)

5.  创建服务。

    1.  在左侧导航栏，选择**服务与路由** \> **服务**。

    2.  在**服务**页面，单击**使用YAML创建资源**。

    3.  在**创建**页面的**模板**代码框输入以下内容，然后单击**创建**。

        ```
        apiVersion: v1
        kind: Service
        metadata:
          labels:
            app: prometheus-go-demo
          name: prometheus-go-demo
        spec:
          ports:
          - name: arms-go-demo
            port: 8077
            protocol: TCP
            targetPort: 8077
          type: NodePort
          selector:
            app: prometheus-go-demo
        ```

    **服务**页面显示创建的服务。

    ![go服务-客户端](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5153455161/p248952.png)


## 步骤四：配置服务发现

配置阿里云Prometheus监控的服务发现以抓取Go应用数据的操作步骤如下：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在设置页面，单击**服务发现**页签，在**服务发现**页签下，单击**ServiceMonitor**页签。

5.  在**ServiceMonitor**页签下，单击**添加ServiceMonitor**。

6.  在**添加ServiceMonitor**对话框中输入以下内容，然后单击**确定**。

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # 填写一个唯一名称
      name: prometheus-go-demo
      # 填写目标命名空间
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # 填写Prometheus Exporter对应的Port的Name字段的值
        port: arms-go-demo
        # 填写Prometheus Exporter对应的Path的值
        path: /metrics
      namespaceSelector:
        any: true
        # Demo的命名空间
      selector:
        matchLabels:
          app: prometheus-go-demo
    ```

    **ServiceMonitor**页签下显示配置的服务发现。

    ![go服务发现](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5153455161/p248955.png)


## 步骤五：配置大盘

配置Grafana大盘以展示数据的操作步骤如下：

1.  打开[Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏选择**+** \> **Import**。

3.  在Import页面的**Import via grafna.com**文本框，输入Prometheus提供的Go应用大盘模板ID6671，然后在其右侧，单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6316294161/p61709.png)

4.  在Import页面输入以下信息，然后单击**Import**。

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6055864161/p63196.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  从**Folder**列表中，选择您的阿里云容器服务K8s集群。

    3.  在**prometheus-apl**下拉框中选择您的阿里云容器服务K8s集群。

    配置完毕后的Grafana大盘如图所示。

    ![ARMS Prometheus Grafana Go](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p63054.png)


## 步骤六：创建Prometheus监控报警

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，单击目标K8s集群的名称。

4.  在左侧导航栏，选择**报警配置**。

5.  在报警配置页面右上角，单击**创建报警**。

6.  在**创建报警**面板，执行以下操作：

    1.  从**告警模板**下拉列表，选择模板。

    2.  在**规则名称**文本框，输入规则名称，例如：网络接收压力报警。

    3.  在**告警表达式**文本框，输入告警表达式。例如：`(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`。

        **说明：** PromQL语句中包含的`$`符号会导致报错，您需要删除包含$符号的语句中`=`左右两边的参数及`=`。例如：将`sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))`修改为`sum (rate (container_network_receive_bytes_total[1m]))`。

    4.  在**持续时间**文本框，输入时间，例如：1分钟，当告警条件连续1分组都满足时才会发送告警。

    5.  在**告警消息**文本框，输入告警消息。

    6.  在**高级配置**的**标签**区域，单击**创建标签**可以设置报警标签，设置的标签可用作分派规则的选项。

    7.  在**高级配置**的**注释**区域，单击**创建注释**，设置键为message，设置值为\{\{变量名\}\}告警信息。设置完成后的格式为：`message:{{变量名}}告警信息`，例如：`message:{{$labels.pod_name}}重启`。

        您可以自定义变量名，也可以选择已有的标签作为变量名。已有的标签包括：

        -   报警规则表达式指标中携带的标签。
        -   通过报警规则创建的标签，请参见[创建报警]()。
        -   ARMS系统自带的默认标签，默认标签说明如下。

            |标签|说明|
            |--|--|
            |alertname|告警名称，格式为：告警名称\_集群名称。|
            |\_aliyun\_arms\_alert\_level|告警等级。|
            |\_aliyun\_arms\_alert\_type|告警类型。|
            |\_aliyun\_arms\_alert\_rule\_id|告警规则对应的ID。|
            |\_aliyun\_arms\_region\_id|地域ID。|
            |\_aliyun\_arms\_userid|用户ID。|
            |\_aliyun\_arms\_involvedObject\_type|关联对象子类型，如ManagedKubernetes，ServerlessKubernetes。|
            |\_aliyun\_arms\_involvedObject\_kind|关联对象分类，如app，cluster。|
            |\_aliyun\_arms\_involvedObject\_id|关联对象ID。|
            |\_aliyun\_arms\_involvedObject\_name|关联对象名称。|

    8.  从**通知策略**下拉列表，选择通知策略。

        如何创建通知策略，请参见[通知策略](/cn.zh-CN/告警管理（新版）/控制台操作/通知策略.md)。

    9.  单击**确定**。

    报警配置页面显示创建的报警。

    ![8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0242584161/p245624.png)


