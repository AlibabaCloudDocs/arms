# Use ARMS Prometheus Monitoring to monitor JVM data

This tutorial describes how to expose JVM data by instrumentation points in applications, capture JVM data by using Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\), and display JVM data on the ARMS Prometheus Grafana dashboard, finally to monitor JVM data with ARMS Prometheus Monitoring.

-   Download the [demo project](https://github.com/liguozhong/prometheus-arms-aliyun-demo)
-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)
-   [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md)

The following figure shows the workflow.

![How it works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61773.png)

## Step 1: Expose JVM data by instrumentation points in applications

Use JVM Exporter to expose JVM data in applications.

1.  Add the following information to the pom.xml file:

    ```
    <dependency>
        <groupId>io.prometheus</groupId>
        <artifactId>simpleclient_hotspot</artifactId>
        <version>0.6.0</version>
    </dependency>
    ```

2.  Add the JVM Exporter dependency in the location where initialization is available.

    For example, add the dependency in the \\src\\main\\java\\com\\monitise\\prometheus\_demo\\DemoController.java file of the demo project.

    ```
    @PostConstruct
        public void initJvmExporter() {
            io.prometheus.client.hotspot.DefaultExports.initialize();
        }
    ```

3.  Expose the Port and Path fields used by Prometheus Monitoring in the \\src\\main\\resources\\application.properties file.

    ```
    management.port: 8081
    endpoints.prometheus.path: prometheus-metrics
    ```

    Enable the HTTP port.

    ```
    @SpringBootApplication
    // Set the Prometheus endpoint /prometheus-metrics
    @EnablePrometheusEndpoint
    // Export the data at /metrics at a Prometheus endpoint.
    @EnableSpringBootMetricsCollector
    public class PrometheusDemoApplication {
        public static void main(String[] args) {
            SpringApplication.run(PrometheusDemoApplication.class, args);
        }
    }
    ```


## Step 2: Deploy the application to the Container Service Kubernetes cluster

Deploy the application to the Container Service Kubernetes cluster so that ARMS Prometheus Monitoring can monitor and capture the JVM data.

1.  Run the following commands in the buildDockerImage.sh file by row:

    ```
    mvn clean install -DskipTests
    docker build -t <name of the local temporary Docker image>:<version of the local temporary Docker image> . --no-cache
    sudo docker tag <name of the local temporary Docker image>:<version of the local temporary Docker image> <registry domain name>/<namespace>/<image name>:<image version>
    sudo docker push <registry domain name>/<namespace>/<image name>:<image version>
    ```

    Example:

    ```
    mvn clean install -DskipTests
    docker build -t promethues-demo:v0 . --no-cache
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    sudo docker push registry.cn-hangzhou.aliyuncs.com/fuling/promethues-demo:v0
    ```

    In this step, a Docker image named promethues-demo is created, and the image is pushed to Alibaba Cloud Docker Registry.

2.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

3.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the target cluster, and click **Dashboard** in the **Actions** column.

    ![Kubernetes cluster console button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61754.png)

4.  In the left-side navigation pane, choose **Workloads** \> **Deployments**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    **Note:** In the following configuration file, values of prometheus.io/port and prometheus.io/path are the ARMS Prometheus Monitoring port and path exposed in [Step 1](#section_0mb_y17_d1o):

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

    In this step, the promethues-demo Docker image created in [1](#step_20d_hjh_aor) is deployed to the Container Service Kubernetes cluster.

5.  In the left-side navigation pane, choose **Discovery and Load Balancing** \> **Services**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

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


## Step 3: Configure ARMS Prometheus Monitoring to capture the JVM data

Configure ARMS Prometheus Monitoring in the ARMS console to capture the JVM data.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located. Find the target cluster, and click **Installation** in the **Actions** column.

4.  After the ARMS Prometheus agent is installed, find the target cluster, and click **Settings** in the **Actions** column.

5.  On the **Details** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following information:

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # Enter a unique name.
      name: tomcat-demo
      # Enter the target namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # Enter the value of the Name field for Port of Prometheus Exporter.
        port: tomcat-monitor
        # Enter the value of the Path field for Prometheus Exporter.
        path: /prometheus-metrics
      namespaceSelector:
        any: true
      selector:
        matchLabels:
          app: tomcat
    ```


## Step 4: Display the JVM data on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 10877 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61711.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the **Select a Prometheus data source** drop-down list.

    After the configuration is complete, the ARMS Prometheus Grafana JVM dashboard appears, as shown in the following figure.

    ![ARMS Prometheus Grafana dashboard for JVM](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7969283851/p61723.png)


## Step 5: Create an alert

1.  You can select one of the two available methods to go to the Create Alarm page.

    -   On the New DashBoard page of the [Prometheus Grafana dashboard](http://grafana.console.aliyun.com/), click theicon to go to the ARMS Prometheus Create Alarm dialog box.
    -   In the left-side navigation pane of the console, choose **Alerts** \> **Alert Policies**. On the Alert Policies page, choose **Create Alarm** \> **Prometheus** in the upper-right corner.
2.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alarm Name such as network receiving pressure alert.

    2.  Select the corresponding **cluster** of the Prometheus monitoring job.

    3.  Set **Type** to **grafana**.

    4.  Select the specific **dashboard** and **chart** to monitor.

    5.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of network receiving bytes \(MB\) is at least 3.

            **Note:** A Grafana chart may contain data of Curve A, Curve B, and Curve C. You can select one of them to monitor.

        3.  In the **PromQL** field, edit the existing PromQL statement or enter a new PromQL statement.

            **Note:** An error may be reported if a PromQL statement contains a dollar sign \($\). You must delete the equal sign \(=\) and the parameters on both sides of the dollar sign \($\) from the statement that contains the dollar sign \($\). For example, modify `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`

    6.  Set Notification Mode. For example, select SMS.

    7.  Set Notification Receiver. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

    ![Prometheus Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3608828061/p61774.png)


After the ARMS Prometheus Grafana JVM dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

[View the metrics of Prometheus Service]()

[Use ARMS Prometheus Monitoring to customize the Grafana dashboard]()

[Create alarms](https://www.alibabacloud.com/help/doc-detail/94833.htm)

