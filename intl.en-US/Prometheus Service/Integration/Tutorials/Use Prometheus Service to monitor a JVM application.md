---
keyword: [Prometheus Service, JVM application monitoring]
---

# Use Prometheus Service to monitor a JVM application

To monitor a Java virtual machine \(JVM\) application by using Prometheus Service, you must instrument the JVM application to expose data, use Prometheus Service to capture the data, configure a Grafana dashboard to display the data, and then create an alert. This topic describes how to use Prometheus Service to monitor a JVM application. In this example, Container Service for Kubernetes \(ACK\) and Container Registry are also used.

-   An ACK cluster is connected to Prometheus Service. For more information, see [Connect an ACK cluster to Prometheus Service]().
-   An image repository is created by using Container Registry. For more information, see [Create an image repository]().

## Demo

You can also use a demo project to learn how to monitor a JVM application by using Prometheus Service. For more information about the demo project, visit [GitHub](https://github.com/liguozhong/prometheus-arms-aliyun-demo).

## Procedure

The following figure shows the process of using Prometheus Service to monitor a JVM application.

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0117484261/p245640.png)

## Step 1: Instrument a JVM application

To instrument the JVM application to expose data, perform the following steps:

1.  Add the Maven dependencies to the pom.xml file.

    ```
    <dependency>
        <groupId>io.prometheus</groupId>
        <artifactId>simpleclient_hotspot</artifactId>
        <version>0.6.0</version>
    </dependency>
    ```

2.  Add the method to initialize the JVM exporter to the application code.

    ```
    @PostConstruct
        public void initJvmExporter() {
            io.prometheus.client.hotspot.DefaultExports.initialize();
        }
    ```

    For more information, see the /src/main/java/com/monitise/prometheus\_demo/DemoController.java file of the demo project.

3.  Configure the port and endpoint that are used to access Prometheus Service in the application.properties file.

    ```
    management.port: 8081
    endpoints.prometheus.path: prometheus-metrics
    ```

    For more information, see the /src/main/resources/application.properties file of the demo project.

4.  Add the method to enable the HTTP port to the application code.

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

    For more information, see the /src/main/java/com/monitise/prometheus\_demo/PrometheusDemoApplication.java file of the demo project.


## Step 2: Upload the JVM application

To build an image for the instrumented JVM application and upload the image to an image repository of Container Registry, perform the following steps:

1.  Run the following command to recompile a module:

    ```
    mvn clean install -DskipTests
    ```

2.  Run the following command to build an image:

    ```
    docker build -t <Name of the on-premises temporary Docker image>:<Version number of the on-premises temporary Docker image> . --no-cache
    ```

    Example:

    ```
    docker build -t promethues-demo:v0 . --no-cache
    ```

3.  Run the following command to tag the image:

    ```
    sudo docker tag <Name of the on-premises temporary Docker image>:<Version number of the on-premises temporary Docker image> <Domain name of the image repository>/<Namespace>/<Image name>:<Image version number>
    ```

    Example:

    ```
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    ```

4.  Run the following command to upload the image to the image repository:

    ```
    sudo docker push <Domain name of the image repository>/<Namespace>/<Image name>:<Image version number>
    ```

    Example:

    ```
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    ```

    You can view the information about the uploaded application image on the **Tags** page of the [Container Registry console](https://cr.console.aliyun.com).

    ![Image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3846798161/p245561.png)


## Step 3: Deploy the JVM application

To deploy the JVM application to an ACK cluster, perform the following steps:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, find the cluster to which you want to deploy the JVM application and click **Applications** in the **Actions** column.

4.  Create a container group.

    1.  In the left-side navigation pane, choose **Workloads** \> **Deployments**.

    2.  On the **Deployments** page, click **Create from YAML** in the upper-right corner.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

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
                image: <Domain name of the image repository>/<Namespace>/<Image name >:<Image version number>
                ports:
                - containerPort: 8080
                  name: tomcat-normal
                - containerPort: 8081
                  name: tomcat-monitor
        ```

        Example:

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

    The **Deployments** page displays the created container group.

    ![Container group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1304898161/p245543.png)

5.  Create a service.

    1.  In the left-side navigation pane, choose **Services and Ingresses** \> **Services**.

    2.  On the **Services** page, click **Create Resources in YAML**.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

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

    The **Services** page displays the created service.

    ![Service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1304898161/p245547.png)


## Step 4: Configure service discovery

To configure service discovery of Prometheus Service to receive data from the JVM application, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the ACK cluster resides. Find the cluster and click **Settings** in the **Actions** column.

4.  On the Settings page, click the **Service Discovery** tab. On the **Service Discovery** tab, click the **ServiceMonitor** tab.

5.  On the **ServiceMonitor** tab, click **Add ServiceMonitor**.

6.  In the **Add ServiceMonitor** dialog box, enter the following code and click **OK**:

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # Enter a unique name.
      name: tomcat-demo
      # Enter a namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
        port: tomcat-monitor
        # Enter the value of the Path field for Prometheus Exporter.
        path: /metrics
      namespaceSelector:
        any: true
        # The namespace of demo.
      selector:
        matchLabels:
          # Enter the value of the Label field in the service.yaml file to find the service.yaml file.
          app: tomcat
    ```

    The **ServiceMonitor** tab displays the configured service discovery task.

    ![Service discovery](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1304898161/p245551.png)


