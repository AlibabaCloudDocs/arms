# Use Prometheus Service to monitor a Go application

To monitor a Go application by using Prometheus Service, you must instrument the Go application to expose data, use Prometheus Service to capture the data, configure a Grafana dashboard to display the data, and then create an alert. This topic describes how to use Prometheus Service to monitor a Go application. In this example, Container Service for Kubernetes \(ACK\) and Container Registry are also used.

Before you begin, make sure that the following requirements are met:

-   An ACK cluster is connected to Prometheus Service. For more information, see [Connect an ACK cluster to Prometheus Service]().
-   An image repository is created by using Container Registry. For more information, see [Create an image repository]().

## Demo

You can also use a demo project to learn how to monitor a Go application by using Prometheus Service. For more information about the demo project, visit [GitHub](https://github.com/liguozhong/prometheus-arms-aliyun-go-demo).

## Procedure

The following figure shows the process of using Prometheus Service to monitor a Go application.

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0117484261/p245640.png)

## Step 1: Instrument a Go application

To instrument the Go application to expose data, perform the following steps:

1.  Import the monitoring package to the Go application.

    ```
    import (
        "fmt"
        "github.com/prometheus/client_golang/prometheus/promhttp"
        "net/http"
        "strconv"
    )
    ```

2.  Associate the HTTP endpoint of Prometheus Service with promhttp.Handler\(\).

    ```
    http.Handle(path, promhttp.Handler()) // Initialize an HTTP handler. 
    ```


## Step 2: Upload the Go application

To build an image for the instrumented Go application and upload the image to an image repository of Container Registry, perform the following steps:

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
    docker build -t prometheus-go-demo:v0 . --no-cache
    ```

3.  Run the following command to tag the image:

    ```
    sudo docker tag <Name of the on-premises temporary Docker image>:<Version number of the on-premises temporary Docker image> <Domain name of the image repository>/<Namespace>/<Image name>:<Image version number>
    ```

    Example:

    ```
    sudo docker tag prometheus-go-demo:v0 registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-go-demo:v0
    ```

4.  Run the following command to upload the image to the image repository:

    ```
    sudo docker push <Domain name of the image repository>/<Namespace>/<Image name>:<Image version number>
    ```

    Example:

    ```
    sudo docker push registry.cn-hangzhou.aliyuncs.com/testnamespace/prometheus-go-demo:v0
    ```

    You can view the information about the uploaded application image on the **Tags** page of the [Container Registry console](https://cr.console.aliyun.com).

    ![Image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3846798161/p245561.png)


## Step 3: Deploy the Go application

To deploy the Go application to an ACK cluster, perform the following steps:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, find the cluster to which you want to deploy the Go application and click **Applications** in the **Actions** column.

4.  Create a container group.

    1.  In the left-side navigation pane, choose **Workloads** \> **Deployments**.

    2.  On the **Deployments** page, click **Create from YAML** in the upper-right corner.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

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
                image: <Domain name of the image repository>/<Namespace>/<Image name >:<Image version number>
                ports:
                - containerPort: 8077
                  name: arms-go-demo
        ```

        Example:

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

    The **Deployments** page displays the created container group.

    ![go-exporter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3846798161/p248949.png)

5.  Create a service.

    1.  In the left-side navigation pane, choose **Services and Ingresses** \> **Services**.

    2.  On the **Services** page, click **Create Resources in YAML**.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

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

    The **Services** page displays the created service.

    ![Go service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3846798161/p248952.png)


## Step 4: Configure service discovery

To configure service discovery of Prometheus Service to receive data from the Go application, perform the following steps:

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
      name: prometheus-go-demo
      # Enter a namespace.
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
        # The namespace of demo.
      selector:
        matchLabels:
          app: prometheus-go-demo
    ```

    The **ServiceMonitor** tab displays the configured service discovery task.

    ![Go service discovery](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3846798161/p248955.png)


## Step 5: Configure a Grafana dashboard

To configure a Grafana dashboard to display data, perform the following steps:

1.  Go to the [homepage of Grafana dashboards](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**.

3.  On the Import page, enter 6671, which is the ID of the Go Grafana template provided by Prometheus, in the **Import via grafna.com** field and click **Load** next to the field.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2116394161/p61709.png)

4.  On the Import page, perform the following operations and click **Import**:

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7116394161/p63196.png)

    1.  Enter a dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **prometheus-apl** drop-down list.

    The following figure shows the configured Grafana dashboard.

    ![ARMS Prometheus Grafana Go](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1128468061/p63054.png)


## Step 6: Create an alert

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


