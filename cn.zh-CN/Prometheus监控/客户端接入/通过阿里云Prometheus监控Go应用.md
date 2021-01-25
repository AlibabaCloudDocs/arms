# 通过阿里云Prometheus监控Go应用

您可以使用阿里云Prometheus监控部署在阿里云K8s集群中的GO应用的运行情况，在监控大盘上查看多种监控数据，还可配置监控报警。本教程介绍如何通过在Go应用中埋点来暴露应用的数据，使用Prometheus抓取数据，并借助Prometheus Grafana大盘来展示数据，最终实现通过Prometheus监控Go应用的目的。

在开始本教程前，确保您已经完成了以下操作：

-   下载[Demo工程](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo)
-   [快速创建Kubernetes托管版集群](/cn.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)
-   [使用私有镜像仓库创建应用](/cn.zh-CN/快速入门/高阶入门/使用私有镜像仓库创建应用.md)

本教程的操作流程如图所示。

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2040633061/p63208.png)

## 步骤一：通过埋点暴露Go应用的数据

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
    http.Handle(path, promhttp.Handler()) //初始化一个HTTP Handler
    ```


## 步骤二：将应用部署至阿里云容器服务K8s集群

1.  逐行运行buildDockerImage.sh中的以下命令，构建名为promethues-arms-aliyun-go-demo的Docker镜像，并将镜像推送至阿里云Docker Registry。

    ```
    mvn clean install -DskipTests
    docker build -t <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> . --no-cache
    sudo docker tag <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    sudo docker push <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    例如：

    ```
    mvn clean install -DskipTests
    docker build -t promethues-arms-aliyun-go-demo:v0.1 . --no-cache
    sudo docker tag promethues-arms-aliyun-go-demo:v0.1 registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-arms-aliyun-go-demo-amd64:dev-v0.1
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0.1
    ```

2.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

3.  在左侧导航栏选择**集群**，在集群列表页面上的目标集群右侧**操作**列单击**应用管理**。

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1230633061/p61754.png)

4.  在**工作负载**页面单击**无状态**页签，在**无状态**页签中，单击**使用模板创建**。

5.  在**使用模板创建**页签中，选择示例模板为自定义，并在文本框中填写以下内容，然后单击**创建**，将步骤[1](#step_20d_hjh_aor)中创建的Docker镜像部署至容器服务K8s集群中。

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: promethues-arms-aliyun-go-demo
    spec:
      replicas: 2
      template:
        metadata:
          labels:
            app: promethues-arms-aliyun-go-demo
        spec:
          containers:
          - name: promethues-arms-aliyun-go-demo
            imagePullPolicy: Always
            image: registry.cn-hangzhou.aliyuncs.com/fuling/prometheus-arms-aliyun-go-demo-amd64:dev-v0.1
            ports:
            - containerPort: 8077
              name: arms-go-demo
    ```

6.  在左侧导航栏选择**服务**，在页面右上角单击**使用YAML创建资源**。

7.  在**工作负载**对应页签中填写以下内容，然后单击**创建**。

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        app: promethues-arms-aliyun-go-demo
      name: promethues-arms-aliyun-go-demo
    spec:
      ports:
      - name: arms-go-demo
        port: 8077
        protocol: TCP
        targetPort: 8077
      type: NodePort
      selector:
        app: promethues-arms-aliyun-go-demo
    ```


## 步骤三：配置Prometheus监控以抓取Go应用的数据

1.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

2.  为目标容器服务K8s集群开启阿里云Prometheus监控。具体操作，请参见[开始使用Prometheus监控]()。

3.  登录[Prometheus控制台](https://prometheus.console.aliyun.com/#/home)。

4.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

5.  在**设置**页面单击**服务发现**页签，在**服务发现**页签上单击**添加ServiceMonitor**，在**添加ServiceMonitor**对话框中填写以下内容，然后单击**确定**。

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # 填写一个唯一名称
      name: promethues-arms-aliyun-go-demo
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
          app: promethues-arms-aliyun-go-demo
    ```


## 步骤四：通过Grafana大盘展示Go应用的数据

最后需要在Prometheus控制台导入Grafana大盘模板并指定Prometheus数据源所在的容器服务K8s集群。

1.  打开[Prometheus Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏中选择**+** \> **Import**，并在**Grafana.com Dashboard**文本框输入6671，然后单击**Load**。

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p61709.png)

3.  在Import页面输入以下信息，然后单击**Import**。

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p63196.png)

    1.  在**Name**文本框中输入自定义的大盘名称。

    2.  从**Folder**列表中，选择您的阿里云容器服务K8s集群。

    3.  在**prometheus-apl**下拉框中选择您的阿里云容器服务K8s集群。

    配置完毕后的Prometheus Grafana Go大盘如图所示。

    ![ARMS Prometheus Grafana Go](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6247219951/p63054.png)


## 步骤五：创建Prometheus监控报警

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在顶部菜单栏选择目标地域，然后单击目标K8s集群名称。

4.  在左侧导航栏中选择**报警配置Beta**，然后在右上角单击**创建报警**。

5.  在**创建报警**对话框中输入以下信息，完成后单击**确认**。

    **说明：** **时间**设置功能暂不支持。

    1.  填写**规则名称**，例如：网络接收压力报警。

    2.  输入报警规则表达式，表达式需要使用PromQL语句。例如：`(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`。

        **说明：** PromQL语句中包含的`$`符号会导致报错，您需要删除包含$符号的语句中`=`左右两边的参数及`=`。例如：将`sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))`修改为`sum (rate (container_network_receive_bytes_total[1m]))`。

    3.  在标签区域单击**创建标签**可以设置报警标签，设置的标签可用作分派规则的选项。

    4.  在注释区域可以编辑告警信息发送模板。单击**创建注释**，设置键为message，设置值为\{\{变量名\}\}告警信息。设置完成后的格式为：message:\{\{变量名\}\}告警信息，例如：message:\{\{$labels.pod\_name\}\}重启。

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

    ![Prometheus-Create alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5347955061/p182018.png)


Prometheus Grafana Go大盘配置完毕后，您可以查看Prometheus监控指标和进一步自定义大盘，详情请参见以下文档。

[查看Prometheus监控指标]()

[通过阿里云Prometheus自定义Grafana大盘]()

**相关文档**  


[什么是Prometheus监控？]()

