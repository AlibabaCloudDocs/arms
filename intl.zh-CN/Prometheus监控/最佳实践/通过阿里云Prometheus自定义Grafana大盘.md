# 通过阿里云Prometheus自定义Grafana大盘

阿里云Prometheus监控可以通过Grafana大盘来展示监控数据，并且支持自定义创建Grafana大盘和从Grafana官网导入大盘两种方式。本文以阿里云容器服务K8s集群和阿里云容器镜像服务为例，介绍通过自定义Grafana大盘展示监控数据。

-   阿里云容器服务K8s集群已接入阿里云Prometheus监控。如何接入，请参见[容器服务Kubernetes版集群]()。
-   已创建阿里云容器镜像服务镜像仓库。如何创建，请参见[创建镜像仓库]()。

## 操作流程

通过阿里云Prometheus自定义Grafana大盘的操作流程如下图所示。

![自定义Grafana大盘](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8947885161/p249448.png)

## 步骤一：上传应用

将应用制作成镜像并上传至阿里云容器镜像服务的镜像仓库的操作步骤如下：

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
    docker build -t promethues-demo:v0 . --no-cache
    ```

3.  执行以下命令为镜像打标。

    ```
    sudo docker tag <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    示例命令：

    ```
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    ```

4.  执行以下命令将镜像推送至镜像仓库。

    ```
    sudo docker push <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    示例命令：

    ```
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    ```

    [容器镜像服务控制台](https://cr.console.aliyun.com)的**镜像版本**页面显示上传的应用镜像。

    ![镜像](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0962584161/p245561.png)


## 步骤二：部署应用

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
          name: prometheus-demo
        spec:
          replicas: 2
          template:
            metadata:
              annotations:
                prometheus.io/scrape: 'true'
                prometheus.io/path: '/prometheus-metrics'
                prometheus.io/port: '8081'
              labels:
                app: tomcat
            spec:
              containers:
              - name: tomcat
                imagePullPolicy: Always
                image: <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
                ports:
                - containerPort: 8080
                  name: tomcat-normal
                - containerPort: 8081
                  name: tomcat-monitor
        ```

        示例代码：

        ```
        apiVersion: apps/v1 # for versions before 1.8.0 use apps/v1beta1
        kind: Deployment
        metadata:
          name: prometheus-demo
          labels:
            app: tomcat
        spec:
          replicas: 2
          selector:
            matchLabels:
              app: tomcat
          template:
            metadata:
              annotations:
                prometheus.io/scrape: 'true'
                prometheus.io/path: '/prometheus-metrics'
                prometheus.io/port: '8081'
              labels:
                app: tomcat
            spec:
              containers:
              - name: tomcat
                imagePullPolicy: Always
                image: registry.cn-hangzhou.aliyuncs.com/peiyu-test/prometheus-demo:v0
                ports:
                - containerPort: 8080
                  name: tomcat-normal
                - containerPort: 8081
                  name: tomcat-monitor
        ```

    **无状态**页面显示创建的容器组。

    ![容器组](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0962584161/p245543.png)

5.  创建服务。

    1.  在左侧导航栏，选择**服务与路由** \> **服务**。

    2.  在**服务**页面，单击**使用YAML创建资源**。

    3.  在**创建**页面的**模板**代码框输入以下内容，然后单击**创建**。

        ```
        apiVersion: v1
        kind: Service
        metadata:
          labels:
            app: tomcat
          name: tomcat
          namespace: default
        spec:
          ports:
          - name: tomcat-normal
            port: 8080
            protocol: TCP
            targetPort: 8080
          - name: tomcat-monitor
            port: 8081
            protocol: TCP
            targetPort: 8081
          type: NodePort
          selector:
            app: tomcat
        ```

    **服务**页面显示创建的服务。

    ![服务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1962584161/p245547.png)


## 步骤三：配置采集规则

阿里云Prometheus会默认监控CPU信息、内存信息、网络信息等。如果您需要监控默认数据外的其他数据，例如订单信息，那么需要为应用自定义Prometheus监控采集规则。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  为应用配置Prometheus监控采集规则分为以下两种情况。

    -   需要监控部署在K8s集群内的应用的业务数据，例如订单信息。操作步骤如下：
        1.  在设置页面，单击**服务发现**页签，在**服务发现**页签下，单击**ServiceMonitor**页签。
        2.  在**ServiceMonitor**页签下，单击**添加ServiceMonitor**。
        3.  在**添加ServiceMonitor**对话框中输入以下内容，然后单击**确定**。

            ```
            apiVersion: monitoring.coreos.com/v1
            kind: ServiceMonitor
            metadata:
              #  填写一个唯一名称
              name: tomcat-demo
              #  填写目标命名空间
              namespace: default
            spec:
              endpoints:
              - interval: 30s
                #  填写service.yaml中Prometheus Exporter对应的Port的Name字段的值
                port: tomcat-monitor
                #  填写Prometheus Exporter对应的Path的值
                path: /metrics
              namespaceSelector:
                any: true
                #  Demo的命名空间
              selector:
                matchLabels:
                  #  填写service.yaml的Label字段的值以定位目标service.yaml
                  app: tomcat
            ```

            **ServiceMonitor**页签下显示配置的服务发现。

            ![服务发现](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1962584161/p245551.png)

    -   需要监控部署在K8s集群之外的业务数据，如Redis连接数。操作步骤如下：
        1.  在设置页面，单击**Prometheus设置**页签。
        2.  在Prometheus.yaml中输入以下内容，然后单击**保存**。

            ```
            global:
              scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
              evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
            scrape_configs:
              - job_name: 'prometheus'
                static_configs:
                - targets: ['localhost:9090']
            ```


## 步骤四：配置大盘

配置Grafana大盘以展示数据的操作步骤如下：

1.  打开[Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏选择**+** \> **Dashboard**。

3.  在New dashboard页面中单击**Add new panel**。

    ![Create Grafana DashBoard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0155864161/p62533.png)

4.  在Edit Panel页面的**Query**区域的下拉列表中选择集群。在**A**折叠面板的**Metrics**下拉列表中选择监控指标，例如：**go\_gc\_duration\_seconds**。

    ![Grafana Add Query](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0155864161/p62736.png)

5.  在页面右侧的区域，填写图表名称，选择大盘的可视化类型，如图形、表格、热点图等，并根据您的需求配置其他参数。

    ![Create Dashboard Visualization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1155864161/p62560.png)

6.  单击右上角**Save**，在弹出的对话框中输入大盘名称，并选择集群，然后单击**Save**。

    您可根据需要自行创建多个大盘和图表。

    ![Save Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1155864161/p62581.png)

    配置完毕后的Grafana大盘如图所示。

    ![ARMS Prometheus Grafana Dashboard to Customize](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2484298951/p62691.png)


## 步骤五：监控复杂指标

如果需要监控涉及复杂运算的指标，您需要在Prometheus监控中进行数据调试，从而得到相应的PromQL语句。

1.  打开[Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏单击**Explore**图标。

3.  在Explore页面顶部下拉框中选择集群，然后在**Metrics**输入框中输入PromQL语句，单击右上角的**Run Query**进行调试。

    ![Prometheus Data Debug](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1155864161/p62734.png)

4.  调试成功后，您可以参考上述步骤继续添加大盘或图表，具体操作，请参见[步骤四：配置大盘](#section_8t5_8w4_779)。


## 步骤六：创建报警

为监控指标创建报警的操作步骤如下：

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

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

    8.  单击**确定**。

    报警配置页面显示创建的报警。


[大盘列表]()

