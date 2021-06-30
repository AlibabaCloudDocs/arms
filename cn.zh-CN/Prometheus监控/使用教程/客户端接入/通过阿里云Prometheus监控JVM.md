---
keyword: [Prometheus监控, JVM监控]
---

# 通过阿里云Prometheus监控JVM

通过在应用中埋点来暴露JVM数据，使用阿里云Prometheus监控采集JVM数据，借助Prometheus Grafana大盘来展示JVM数据，并创建报警，即可实现利用Prometheus监控JVM的目的。本文以阿里云容器服务K8s集群和阿里云容器镜像服务为例，介绍如何通过Prometheus监控JVM。

-   阿里云容器服务K8s集群已接入阿里云Prometheus监控。如何接入，请参见[容器服务Kubernetes版集群]()。
-   已创建阿里云容器镜像服务镜像仓库。如何创建，请参见[创建镜像仓库]()。

## Demo

如需快速体验如何通过Prometheus监控JVM，您可以使用已埋点的[Demo项目](https://github.com/liguozhong/prometheus-arms-aliyun-demo)。

## 操作流程

通过阿里云Prometheus监控JVM的操作流程如下图所示。

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3649944261/p245640.png)

## 步骤一：为应用埋点

为应用埋点以暴露JVM数据的操作步骤如下：

1.  在pom.xml文件中添加Maven依赖。

    ```
    <dependency>
        <groupId>io.prometheus</groupId>
        <artifactId>simpleclient_hotspot</artifactId>
        <version>0.6.0</version>
    </dependency>
    ```

2.  在应用代码中添加初始化JVM Exporter的方法。

    ```
    @PostConstruct
        public void initJvmExporter() {
            io.prometheus.client.hotspot.DefaultExports.initialize();
        }
    ```

    您可以参考Demo项目的/src/main/java/com/monitise/prometheus\_demo/DemoController.java文件。

3.  在application.properties文件中配置用于Prometheus监控的端口和路径。

    ```
    management.port: 8081
    endpoints.prometheus.path: prometheus-metrics
    ```

    您可以参考Demo项目的/src/main/resources/application.properties文件。

4.  在应用代码中添加打开HTTP端口的方法。

    ```
    @SpringBootApplication
    // sets up the prometheus endpoint /prometheus-metrics
    @EnablePrometheusEndpoint
    // exports the data at /metrics at a prometheus endpoint
    @EnableSpringBootMetricsCollector
    public class PrometheusDemoApplication {
        public static void main(String[] args) {
            SpringApplication.run(PrometheusDemoApplication.class, args);
        }
    }
    ```

    您可以参考Demo项目的/src/main/java/com/monitise/prometheus\_demo/PrometheusDemoApplication.java文件。


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


## 步骤四：配置服务发现

通过ServiceMonitor配置阿里云Prometheus监控的服务发现以采集JVM数据。具体操作，请参见[通过ServiceMonitor创建服务发现]()。

