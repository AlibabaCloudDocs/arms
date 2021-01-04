---
keyword: [Prometheus Monitoring, JVM application monitoring]
---

# Use ARMS Prometheus Monitoring to monitor JVM applications

This topic describes how to use ARMS Prometheus Monitoring to monitor a JVM application. For monitoring purposes, you must instrument a JVM application to expose the data to ARMS Prometheus Monitoring, configure ARMS Prometheus Monitoring to capture data of the JVM application, customize an ARMS Prometheus Grafana dashboard to display the data, and then configure an alert. A JVM application in a Container Service for Kubernetes \(ACK\) cluster is used in this example.

Before you begin, make sure that the following requirements are met:

-   A demo project is downloaded. Download link: [prometheus-arms-aliyun-demo](https://github.com/liguozhong/prometheus-arms-aliyun-demo).
-   A managed ACK cluster is created. For more information, see [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md).
-   An application is created from a private image repository. For more information, see [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md).

## Procedure

The following figure shows the workflow.

![How it works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61773.png)

## Step 1: Instrument a JVM application to expose the data to ARMS Prometheus Monitoring

You must use the JVM exporter to expose the data in the JVM application.

To expose the data, perform the following operations:

1.  Add the Maven dependencies to the pom.xml file.

    ```
    <dependency>
        <groupId>io.prometheus</groupId>
        <artifactId>simpleclient_hotspot</artifactId>
        <version>0.6.0</version>
    </dependency>
    ```

2.  Add the method to initialize the JVM exporter to the locaiton where initialization can be performed.

    For example, add the dependency to the /src/main/java/com/monitise/prometheus\_demo/DemoController.java file of the demo project.

    ```
    @PostConstruct
        public void initJvmExporter() {
            io.prometheus.client.hotspot.DefaultExports.initialize();
        }
    ```

3.  Configure the Port and Path fields that are used by ARMS Prometheus Monitoring in the /src/main/resources/application.properties file.

    ```
    management.port: 8081
    endpoints.prometheus.path: prometheus-metrics
    ```

4.  Enable the HTTP port in the /src/main/java/com/monitise/prometheus\_demo/PrometheusDemoApplication.java file.

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


## Step 2: Deploy the application to an ACK cluster

You must deploy the JVM application to an ACK cluster. This is the prerequisite to capture data of the JVM application by using ARMS Prometheus Monitoring.

To deploy the JVM application, perform the following operations:

1.  Run the following commands in the buildDockerImage.sh file of the demo project line by line to create a Docker image named promethues-demo and push the image to Alibaba Cloud Container Registry.

    ```
    mvn clean install -DskipTests
    docker build -t <Name of the local temporary Docker image>:<Version of the local temporary Docker image> . --no-cache
    sudo docker tag <Name of the local temporary Docker image>:<Version of the local temporary Docker image> <Registry domain name>/<Namespace>/<Image name>:<Image version>
    sudo docker push <Registry domain name>/<Namespace>/<Image name>:<Image version>
    ```

    Example:

    ```
    mvn clean install -DskipTests
    docker build -t promethues-demo:v0 . --no-cache
    sudo docker tag promethues-demo:v0 registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0
    ```

2.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

3.  In the left-side navigation pane, click **Clusters**. On the Clusters page, find the cluster in which you want to deploy the application and click **Applications** in the **Actions** column.

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9273229061/p61754.png)

4.  On the **Workloads** page, click the **Deployments** tab. On the **Deployments** tab, click **Create from Template**.

5.  On the **Create from Template** tab, select Custom from the Sample Template drop-down list. In the Template text editor, enter the following text. Then, click **Create** to deploy the Docker image that was created in [1](#step_20d_hjh_aor) to the ACK cluster.

    **Note:** Values of prometheus.io/port and prometheus.io/path in the following configuration file are the ARMS Prometheus Monitoring port and path exposed in [Step 1](#section_0mb_y17_d1o):

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

6.  In the left-side navigation pane, choose Services and Ingresses \> **Services**. In the upper-right corner of the Services page, click **Create Resources in YAML**.

7.  In the Template text editor on the **Workloads** tab, enter the following text. In the lower part of the page, click **Create**.

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


## Step 3: Configure ARMS Prometheus Monitoring to capture data of the JVM application

To capture data of the JVM application, perform the following operations:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  Enable ARMS Prometheus Monitoring for the ACK cluster. For more information, see [Get started with Prometheus Service]().

3.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

4.  In the left-side navigation pane, click **Prometheus Monitoring**.

5.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the ACK cluster is deployed. Find the cluster and click **Settings** in the **Actions** column.

6.  On the page that appears, click the **Service Discovery** tab. On the **Service Discovery** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following content and click **OK**:****

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # Enter a unique name.
      name: tomcat-demo
      # Enter the desired namespace.
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
        # Demo namespace:
      selector:
        matchLabels:
          # Enter the value of the Label field in the service.yaml file to find the service.yaml file.
          app: tomcat
    ```


## Step 4: Present data of the JVM application on the Grafana dashboard

Import the Grafana dashboard template and specify the ACK cluster where the Prometheus data source is located.

1.  Go to the homepage of [ARMS Prometheus Grafana](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 10877 in the **Import via grafana.com** field, and then click **Load**.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, configure the following parameters and click **Import**:

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61711.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **Select a Prometheus data source** drop-down list.

    After the parameters are configured, the Prometheus Grafana Go dashboard appears, as shown in the following figure.

    ![ARMS Prometheus Grafana Dashboard for JVM](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7969283851/p61723.png)


## Step 5: Create a Prometheus Monitoring alert

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar, select a region. Then, click the name of the required Kubernetes cluster.

4.  In the left-side navigation pane, choose **Alarm configuration beta**. Then, click **Create Alert** in the upper-right corner.

5.  In the **Create Alert** dialog box, configure the following parameters, and then click **OK**.

    **Note:** The **Time** parameter is not supported.

    1.  Enter a name in the **Rule Name** field. Example: alerts for inbound traffic.

    2.  Enter an expression that uses a PromQL statement. Example: `(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`.

        **Note:** An error may be reported if a PromQL statement contains a dollar sign \(`$`\). You must remove the equal sign \(`=`\) and the parameters on both sides of the equal sign \(`=`\) from the statement that contains the dollar sign \($\). For example, change `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`.

    3.  In the Labels section, click **Create Tag** to specify alert tags. The specified tags can be used as options for a dispatch rule.

    4.  In the Annotations section, specify a template for alert messages. Click **Create Annotation**. Set Key to message and Value to \{\{variable name\}\} alert message. The specified annotation is in the format of message:\{\{variable name\}\} alert notification. Example: message:\{\{$labels.pod\_name\}\} restart.

        You can customize a variable name or select an existing tag as the variable name. Existing tags:

        -   The tags that are carried in the metrics of an alert rule expression.
        -   The tags that are created when you create an alert rule. For more information, see [Create an alert]().
        -   The default tags provided by ARMS. The following table describes the default tags.

            |Tag|Description|
            |---|-----------|
            |alertname|The name of the alert. The format is <Alert name\>\_<Cluster name\>.|
            |\_aliyun\_arms\_alert\_level|The level of the alert.|
            |\_aliyun\_arms\_alert\_type|The type of the alert.|
            |\_aliyun\_arms\_alert\_rule\_id|The ID of the alert rule.|
            |\_aliyun\_arms\_region\_id|The ID of the region.|
            |\_aliyun\_arms\_userid|The ID of the user.|
            |\_aliyun\_arms\_involvedObject\_type|The subtype of the associated object, for example, ManagedKubernetes or ServerlessKubernetes.|
            |\_aliyun\_arms\_involvedObject\_kind|The type of the associated object, for example, app or cluster.|
            |\_aliyun\_arms\_involvedObject\_id|The ID of the associated object.|
            |\_aliyun\_arms\_involvedObject\_name|The name of the associated object.|

    ![Prometheus-Create alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2026378061/p182018.png)


## What to do next

After the ARMS Prometheus Grafana JVM dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following topics:

[View Prometheus Monitoring metrics]()

[Use ARMS Prometheus Monitoring to customize Grafana dashboards]()

[Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md)

