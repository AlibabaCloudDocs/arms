# 通过 ARMS Prometheus 监控 JVM {#task_2277600 .task}

通过在应用中埋点来暴露 JVM 数据，使用 ARMS Prometheus 监控抓取 JVM 数据，并借助 ARMS Prometheus Grafana 大盘来展示 JVM 数据，即可实现通过 ARMS Prometheus 监控 JVM 的目的。

-   下载 [Demo 工程](https://github.com/liguozhong/prometheus-arms-aliyun-demo)
-   [快速创建Kubernetes集群](../../../../../intl.zh-CN/快速入门/基础入门/快速创建Kubernetes集群.md#)
-   [创建容器镜像](../../../../../intl.zh-CN/用户指南/构建管理/构建容器镜像.md#)

本教程的操作流程如图所示。

![How it works](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1806048/156897614961773_zh-CN.png)

## 步骤一：通过埋点暴露 JVM 数据 {#section_0mb_y17_d1o .section}

首先需要在应用中使用 JVM Exporter 暴露 JVM 数据。

1.  在 pom.xml 文件中添加以下依赖。 

    ``` {#codeblock_njq_ihu_09w}
    <dependency>
        <groupId>io.prometheus</groupId>
        <artifactId>simpleclient_hotspot</artifactId>
        <version>0.6.0</version>
    </dependency>
    ```

2.  在可以执行初始化的位置添加对 JVM Exporter 的依赖。 

    例如 Demo 工程的 \\src\\main\\java\\com\\monitise\\prometheus\_demo\\DemoController.java 文件。

    ``` {#codeblock_xpu_30o_2a8}
    @PostConstruct
        public void initJvmExporter() {
            io.prometheus.client.hotspot.DefaultExports.initialize();
        }
    ```

3.  在 \\src\\main\\resources\\application.properties 文件中暴露用于 Prometheus 监控的端口（Port）和路径（Path）。 

    ``` {#codeblock_v0d_br8_511}
    management.port: 8081
    endpoints.prometheus.path: prometheus-metrics
    ```


## 步骤二：将应用部署至阿里云容器服务 K8s 集群 {#section_vkv_htv_izb .section}

其次需要将应用部署至容器服务 K8s 集群，以便 ARMS Prometheus 监控抓取 JVM 数据。

1.  逐行运行 buildDockerImage.sh 中的以下命令。 

    ``` {#codeblock_qra_cb0_vtp}
    mvn clean install -DskipTests
    docker build -t <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> . --no-cache
    sudo docker tag <本地临时Docker镜像名称>:<本地临时Docker镜像版本号> <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    sudo docker push <Registry域名>/<命名空间>/<镜像名称>:<镜像版本号>
    ```

    例如：

    ``` {#codeblock_lc1_wr4_uzi}
    mvn clean install -DskipTests
    docker build -t promethues-demo:v0 . --no-cache
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    sudo docker push registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    ```

    此步骤会构建 Docker 镜像，并将镜像推送至阿里云 Docker Registry。

2.  登录[容器服务 Kubernetes 版控制台](https://cs.console.aliyun.com/#/k8s/overview)。
3.  在左侧导航栏选择**集群** \> **集群**，在集群列表页面上的目标集群右侧**操作**列单击**控制台**。 

    ![K8s Cluster Console Button](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1806048/156897614961754_zh-CN.png)

4.  在左侧导航栏选择**工作负载** \> **部署**，在页面右上角单击**创建**，并在**使用文本创建**页签上填写以下内容。 

    **说明：** 以下配置文件中的 prometheus.io/port 和 prometheus.io/path 的值分别为[步骤一：通过埋点暴露 JVM 数据](#section_0mb_y17_d1o)中暴露的 Prometheus 监控端口和路径。

    ``` {#codeblock_olz_x13_sph}
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

    此步骤将步骤 [1](#step_20d_hjh_aor) 中的 Docker 镜像部署至容器服务 K8s 集群中。

5.  在左侧导航栏选择**服务发现与负载均衡** \> **服务**，在页面右上角单击**创建**，并在**使用文本创建**页签上填写以下内容。 

    ``` {#codeblock_79b_pns_wm1}
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


## 步骤三：配置 ARMS Prometheus 监控以抓取 JVM 数据 {#section_nn8_wk6_v53 .section}

接下来需要在 ARMS 控制台配置 ARMS Prometheus 监控以抓取 JVM 数据。

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。
2.  在左侧导航栏中单击 **Prometheus监控**。
3.  在 **Prometheus监控**页面顶部选择容器服务 K8s 集群所在的地域，并在目标集群右侧的**操作**列单击**安装**。
4.  ARMS Prometheus Agent 安装完毕后，在目标集群右侧的**操作**列单击**设置**。
5.  在**配置详情**页签上单击**添加ServiceMonitor**，在**新增ServiceMonitor** 对话框中填写以下内容。 

    ``` {#codeblock_lkd_1od_8yu}
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # 填写一个唯一名称
      name: tomcat-demo
      # 填写目标命名空间
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # 填写 Prometheus Exporter 对应的 Port 的 Name 字段的值
        port: tomcat-monitor
        # 填写 Prometheus Exporter 对应的 Path 的值
        path: /prometheus-metrics
      namespaceSelector:
        any: true
      selector:
        matchLabels:
          app: tomcat
    ```


## 步骤四：通过 Grafana 大盘展示 JVM 数据 {#section_eud_043_604 .section}

最后需要在 ARMS 控制台导入 Grafana 大盘模板并指定 Prometheus 数据源所在的容器服务 K8s 集群。

1.  打开 [ARMS Prometheus Grafana 大盘概览页](http://arms-prom-grafana-hz.aliyun.com)。
2.  在左侧导航栏中选择 **+** \> **Import**，并在 **Grafana.com Dashboard** 文本框输入 10877，然后单击 Load。 

    ![Import Grafana Dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1806048/156897615061709_zh-CN.png)

3.  在 Import 页面输入以下信息，然后单击 **Import**。 

    ![Import Grafana Dashboard with Options](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1806048/156897615061711_zh-CN.png)

    1.  在 **Name** 文本框中输入自定义的大盘名称。
    2.  在 **Folder** 下拉框中选择您的阿里云容器服务 K8s 集群。
    3.  在 **Select a Prometheus data source** 下拉框中选择您的阿里云容器服务 K8s 集群。

配置完毕后的 ARMS Prometheus Grafana JVM 大盘如图所示。

![ARMS Prometheus Grafana Dashboard for JVM](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1806048/156897615061723_zh-CN.png)

ARMS Prometheus Grafana JVM 大盘配置完毕后，您可以查看 Prometheus 监控指标和进一步自定义大盘，详见相关文档。

**相关文档**  


[查看 Prometheus 监控指标](intl.zh-CN/Prometheus 监控/查看 Prometheus 监控指标.md#)

