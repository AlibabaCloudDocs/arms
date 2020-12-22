# Use ARMS Prometheus Monitoring to monitor MySQL data

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to monitor MySQL by capturing MySQL data and displaying the captured data on the ARMS Prometheus Grafana dashboard.

-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)
-   [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md)

The following figure shows the workflow.

![How it works](../images/p62667.png)

## Step 1: Capture MySQL data through an external application

Deploy an application by using the mysqld-exporter image officially provided by Prometheus to the Container Service Kubernetes cluster to capture MySQL data.

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the target cluster, and click **Dashboard** in the **Actions** column.

    ![Kubernetes cluster console button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61754.png)

3.  In the left-side navigation pane, choose **Workloads** \> **Deployments**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    **Note:** Change the values of <yourMySQLUsername\>, <yourMySQLPassword\>, <IP\>, and <port\> to those of MySQL.

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

    In this step, the mysqld-exporter application is deployed to the Container Service Kubernetes cluster.

4.  In the left-side navigation pane, choose **Discovery and Load Balancing** \> **Services**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

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


## Step 2: Configure ARMS Prometheus Monitoring to receive MySQL data

Configure ARMS Prometheus Monitoring in the ARMS console to receive MySQL data captured through external applications.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located. Find the target cluster, and click **Installation** in the **Actions** column.

4.  After the ARMS Prometheus agent is installed, find the target cluster, and click **Settings** in the **Actions** column.

5.  On the **Details** tab, click **Add ServiceMonitor**. In the **Add ServiceMonitor** dialog box, enter the following information:

    ```
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      labels:
        app: mysqld-exporter
        release: p
      name: mysqld-exporter
    # namespace: monitoring
    # The Prometheus namespace
    spec:
      endpoints:
      - interval: 30s
        # The Mysqld Grafana template ID is 7362.
        # Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
        port: mysqld-exporter
        # Enter the path exposed in Prometheus Exporter code.
        path: /metrics
      namespaceSelector:
        any: true
        # The namespace of the NGINX Demo
      selector:
        matchLabels:
          app: mysqld-exporter
    ```


## Step 3: Display the MySQL data on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 7362 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](../images/p62645.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the **prometheus** drop-down list.

    After the configuration is complete, the ARMS Prometheus Grafana MySQL dashboard appears, as shown in the following figure.

    ![ARMS Prometheus Grafana MySQL](../images/p62727.png)


## Step 4: Create an alert

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


After the ARMS Prometheus Grafana MySQL dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

**Related topics**  


[View the metrics of Prometheus Service]()

[Use ARMS Prometheus Monitoring to customize the Grafana dashboard]()

[Create alarms](https://www.alibabacloud.com/help/doc-detail/94833.htm)

