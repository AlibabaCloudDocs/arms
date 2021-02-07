# Use ARMS Prometheus Monitoring to monitor Go applications

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to monitor the running status of Go applications deployed in Container Service for Kubernetes clusters, view various monitoring data on a dashboard, and configure alerts. This topic describes how to use ARMS Prometheus Monitoring to monitor a Go application. For monitoring purposes, you must instrument a Go application to expose the data to ARMS Prometheus Monitoring, configure ARMS Prometheus Monitoring to capture data of the Go application, and then customize an ARMS Prometheus Grafana dashboard to display the data.

Before you begin, make sure that the following requirements are met:

-   A demo project is downloaded. Download link: [prometheus-arms-aliyun-go-demo](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo).
-   A managed ACK cluster is created. For more information, see [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md).
-   An application from a private image repository is created. For more information, see [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md).

The following figure shows the workflow.

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4689762161/p63208.png)

## Step 1: Instrument a Go application to expose the data to ARMS Prometheus Monitoring

1.  Import the monitoring package to the Go application.

    ```
    import (
        "fmt"
        "github.com/prometheus/client_golang/prometheus/promhttp"
        "net/http"
        "strconv"
    )
    ```

2.  Associate the HTTP endpoint of Prometheus Monitoring with promhttp.Handler\(\).

    ```
    http.Handle(path, promhttp.Handler()) //Initialize an HTTP handler.
    ```


## Step 2: Deploy the Go application to a Container Service for Kubernetes \(ACK\) cluster

1.  Run the following commands in the buildDockerImage.sh file line by line to create a Docker image named promethues-arms-aliyun-go-demo and push the image to Alibaba Cloud Docker Registry:

    ```
    mvn clean install -DskipTests
    docker build -t <Name of the local temporary Docker image>:<Version of the local temporary Docker image> . --no-cache
    sudo docker tag <Name of the local temporary Docker image>:<Version of the local temporary Docker image> <Registry domain name>/<Namespace>/<Image name>:<Image version>
    sudo docker push <Registry domain name>/<Namespace>/<Image name>:<Image version>
    ```

    Example:

    ```
    mvn clean install -DskipTests
    docker build -t promethues-arms-aliyun-go-demo:v0.1 . --no-cache
    sudo docker tag promethues-arms-aliyun-go-demo:v0.1 registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-arms-aliyun-go-demo-amd64:dev-v0.1
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/promethues-demo:v0.1
    ```

2.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

3.  In the left-side navigation pane, click **Clusters**. On the Clusters page, find the cluster in which you want to deploy the application and click **Applications** in the **Actions** column.

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9273229061/p61754.png)

4.  On the **Workloads** page, click the **Deployments** tab. On the **Deployments** tab, click **Create from Template**.

5.  On the **Create from Template** tab, select Custom from the Sample Template drop-down list. In the Template text editor, enter the following text. Then, click **Create** to deploy the Docker image that was created in [1](#step_20d_hjh_aor) to the ACK cluster.

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

6.  In the left-side navigation pane, choose Services and Ingresses \> **Services**. In the upper-right corner of the Services page, click **Create Resources in YAML**.

7.  In the Template text editor, enter the following text. In the lower part of the page, click **Create**.

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


## Step 3: Configure ARMS Prometheus Monitoring to capture data of the Go application

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  Enable ARMS Prometheus Monitoring for the ACK cluster. For more information, see [Get started with Prometheus Service]().

3.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

4.  In the left-side navigation pane, click **Prometheus Monitoring**.

5.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the ACK cluster is deployed. Find the cluster and click **Settings** in the **Actions** column.

6.  On the page that appears, click the **Service Discovery** tab. On the **Service Discovery** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following content and click **OK**.

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      # Enter a unique name.
      name: promethues-arms-aliyun-go-demo
      # Enter the desired namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # Enter the value of the Name field for Port of Prometheus Exporter.
        port: arms-go-demo
        # Enter the value of the Path field for Prometheus Exporter.
        path: /metrics
      namespaceSelector:
        any: true
        # Demo namespace.
      selector:
        matchLabels:
          app: promethues-arms-aliyun-go-demo
    ```


## Step 4: Present data of the Go application on the Grafana dashboard

Import the Grafana dashboard template and specify the ACK cluster where the Prometheus data source is located.

1.  Go to the homepage of [ARMS Prometheus Grafana](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 6671 in the **Import via grafana.com** field, and then click **Load**.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, configure the following parameters and click **Import**:

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0128468061/p63196.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **prometheus-apl** drop-down list.

    After the parameters are configured, the Prometheus Grafana Go dashboard appears, as shown in the following figure.

    ![ARMS Prometheus Grafana Go](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1128468061/p63054.png)


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


After the ARMS Prometheus Grafana Go dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following topics:

[View Prometheus Monitoring metrics]()

[Use ARMS Prometheus Monitoring to customize Grafana dashboards]()

**Related topics**  


[What is Prometheus Service?]()

