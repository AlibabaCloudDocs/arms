# 通过阿里云Prometheus自定义Grafana大盘

阿里云Prometheus监控可以通过Prometheus Grafana大盘来展示监控数据，并且支持自定义创建Grafana大盘和从Grafana官网导入大盘两种方式。本文主要介绍自定义Grafana大盘来展示监控数据的方式。

[快速创建Kubernetes托管版集群](/intl.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)

## 步骤一：将应用部署至阿里云容器服务K8s集群

首先需要将应用部署至容器服务K8s集群，以便Prometheus监控抓取JVM数据。

1.  逐行运行buildDockerImage.sh中的以下命令。

    ```
    mvn clean install -DskipTests
    docker build -t <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> . --no-cache
    sudo docker tag <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    sudo docker push <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    例如：

    ```
    mvn clean install -DskipTests
    docker build -t promethues-demo:v0 . --no-cache
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    sudo docker push registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    ```

    此步骤构建了名为promethues-demo的Docker镜像，并将镜像推送至阿里云Docker Registry。

2.  登录[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)。

3.  在左侧导航栏选择**集群**，在集群列表页面上的目标集群右侧**操作**列单击**应用管理**。

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1230633061/p61754.png)

4.  在**工作负载**页面单击**无状态**页签，在**无状态**页签中，单击**使用模板创建**。

5.  在**使用模板创建**页签中，选择示例模板为自定义，并在文本框中填写以下内容，然后单击**创建**，将promethues-demo部署至容器服务K8s集群中。

    **说明：** 以下配置文件中的prometheus.io/port和prometheus.io/path的值分别为应用中暴露的Prometheus监控端口和路径。

    ```
    apiVersion: extensions/v1beta1
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
            image: registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
            ports:
            - containerPort: 8080
              name: tomcat-normal
            - containerPort: 8081
              name: tomcat-monitor
    ```

6.  在左侧导航栏选择**服务**，在页面右上角单击**使用YAML创建资源**。

7.  在**工作负载**对应页签中填写以下内容，然后单击**创建**。

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        name: tomcat
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


## 步骤二：为应用安装Prometheus Agent

为应用所在的目标容器服务K8s集群开启阿里云Prometheus监控。具体操作，请参见[开始使用Prometheus监控]()。

## 步骤三：为应用配置Prometheus监控采集规则

Prometheus Agent安装完成后，会默认监控CPU信息、内存信息、网络信息等。如果您需要监控默认数据外的其他数据，例如订单信息，那么需要为应用配置Prometheus监控采集规则。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面中目标集群右侧的**操作**列单击**设置**。

4.  为应用配置Prometheus监控采集规则分为以下两种情况。

    -   如果您需要监控部署在K8s集群内的应用的业务数据，例如订单信息，可以在**服务发现**页签上单击**添加ServiceMonitor**，并在**添加ServiceMonitor**对话框中参考以下示例内容进行填写，然后单击**确定**。

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

    -   如果您需要监控部署在K8s集群之外的业务数据，如Redis连接数时，可以在**Prometheus设置**页签上参考以下示例内容进行填写，然后单击**保存**。

        ```
        global:
          scrape_interval:     15s
          evaluation_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
            - targets: ['localhost:9090']
        ```


## 步骤四：自定义创建Grafana大盘

1.  打开[Prometheus Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏中选择**+** \> **Dashboard**，并在**New Panel**区域框中单击**Add Query**。

    ![Create Grafana DashBoard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1484298951/p62533.png)

3.  在**Query**右侧的下拉列表中选择集群。在**A**折叠面板的**Metrics**下拉列表中选择监控指标，例如：**go\_gc\_duration\_seconds**。

    ![Grafana Add Query](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1484298951/p62736.png)

4.  单击页面左侧的图表图标，选择大盘的可视化类型，如图形、表格、热点图等，并根据您的需求配置其他参数。

    ![Create Dashboard Visualization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1484298951/p62560.png)

5.  单击页面左侧的设置图标，填写图表名称。

    ![Set Visualization General](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2484298951/p62566.png)

6.  创建Prometheus监控告警，具体操作，请参见[创建报警]()。

7.  单击右上角的保存图标，在Save As...对话框中输入大盘名称，并选择集群，然后单击**Save**保存大盘和图表。您可根据需要自行创建多个大盘和图表。

    ![Save Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2484298951/p62581.png)


## 步骤五：进行数据调试监控复杂指标

如果需要监控涉及复杂运算的指标，您需要在Prometheus监控中进行数据调试，从而得到相应的PromQL语句。

1.  打开[Prometheus Grafana大盘概览页](http://g.console.aliyun.com/)。

2.  在左侧导航栏单击**Explore**图标。

3.  在Explore页面的**Metrics**输入框中输入PromQL语句进行调试。

    ![Prometheus Data Debug](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2484298951/p62734.png)

4.  调试成功后，您可以参考上述步骤继续添加大盘或图表，具体操作，请参见[步骤四：自定义创建Grafana大盘](#section_8t5_8w4_779)。


配置完毕后的Prometheus Grafana大盘如图所示。

![ARMS Prometheus Grafana Dashboard to Customize](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2484298951/p62691.png)

[查看Prometheus监控指标]()

[通过阿里云Prometheus监控JVM]()

