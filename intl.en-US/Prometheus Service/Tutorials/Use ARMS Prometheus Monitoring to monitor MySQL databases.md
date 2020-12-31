# Use ARMS Prometheus Monitoring to monitor MySQL databases

ARMS Prometheus monitoring allows you to monitor MySQL databases by capturing data from the databases and presenting the captured data on the ARMS Prometheus Grafana dashboard.

-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)
-   [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md)

The following figure shows the workflow.

![How It Works](../images/p149087.png)

## Step 1: Capture data from a MySQL database by using an external application

Deploy the mysqld-exporter image provided by Prometheus to a Container Service for Kubernetes \(ACK\) cluster to capture MySQL data.

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**. On the Clusters page, click **Applications** in the **Actions** column corresponding to the cluster.

    ![K8s Cluster Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9273229061/p61754.png)

3.  On the **Workloads** page, click the **Deployments** tab. On the **Deployments** tab, click **Create from Template**.

4.  On the **Create from Template** tab, select Custom from the Sample Template drop-down list. Enter the following text into the Template text editor and click **Create** to deploy the mysqld-exporter application to the ACK cluster.

    **Note:** Replace the values of <yourMySQLUsername\>, <yourMySQLPassword\>, <IP\>, and <port\> with the corresponding values of the MySQL database.

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: mysqld-exporter
    spec:
      replicas: 1
      template:
        metadata:
          labels:
            app: mysqld-exporter
        spec:
          containers:
          - name: mysqld-exporter
            imagePullPolicy: Always
            env:
              - name: DATA_SOURCE_NAME
                value: "<yourMySQLUsername>:<yourMySQLPassword>@(<IP>:<port>)/"
            image: prom/mysqld-exporter
            ports:
            - containerPort: 9104
              name: mysqld-exporter
    ```

5.  In the left-side navigation pane, choose Services and Ingresses \> **Services**. On the Services page, click **Create Resources in YAML**.

6.  On the **Workloads** tab, enter the following text in the Template text editor and click **Create**:

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        app: mysqld-exporter
      name: mysqld-exporter
    spec:
      ports:
      - name: mysqld-exporter
        port: 9104
        protocol: TCP
        targetPort: 9104
      type: NodePort
      selector:
        app: mysqld-exporter
    ```


## Step 2: Configure ARMS Prometheus Monitoring to receive data from the MySQL database

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  Enable ARMS Prometheus Monitoring for the ACK cluster. For more information, see [Get started with Prometheus Service]().

3.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

4.  In the left-side navigation pane, click **Prometheus Monitoring**.

5.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where your ACK cluster is deployed. Find the cluster and click **Settings** in the **Actions** column.

6.  On the **Settings** page, click the **Service Discovery** tab. On the **Service Discovery** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following content and click **OK**:

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      labels:
        app: mysqld-exporter
        release: p
      # Enter a unique name.
      name: mysqld-exporter
      # Enter the desired namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # The Mysqld Grafana template ID is 7362.
        # Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
        port: mysqld-exporter
        # Enter the value of the Path field for Prometheus Exporter.
        path: /metrics
      namespaceSelector:
        any: true
        # Demo namespace:
        matchLabels:
          app: mysqld-exporter
    ```


## Step 3: Present data of the MySQL database on the Grafana dashboard

Import the Grafana dashboard template and specify the ACK cluster where the Prometheus data source is located.

1.  Go to [Prometheus Grafana](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 7362 in the **Import via grafana.com** field, and then click **Load**.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, configure the following parameters and click **Import**.

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1377468061/p62645.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **prometheus** drop-down list.

    After the parameters are configured, the Prometheus Grafana MySQL dashboard is displayed as shown in the following figure.

    ![ARMS Prometheus Grafana MySQL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1377468061/p62727.png)


## Step 4: Create a Prometheus Monitoring alert

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


After the ARMS Prometheus Grafana MySQL dashboard is configured, you can view metrics of Prometheus Monitoring and customize the dashboard. For more information, see the following topics.

[View Prometheus Monitoring metrics]()

[Use ARMS Prometheus Monitoring to customize Grafana dashboards]()

[Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md)

