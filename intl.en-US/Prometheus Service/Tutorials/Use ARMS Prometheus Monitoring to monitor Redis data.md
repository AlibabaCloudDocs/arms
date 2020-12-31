# Use ARMS Prometheus Monitoring to monitor Redis data

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) allows you to monitor Redis by capturing Redis data and displaying the captured data on the ARMS Prometheus Grafana dashboard.

-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md)
-   [Create an application from a private image repository](/intl.en-US/Quick Start/Advanced operations/Create an application from a private image repository.md)

## Step 1: Capture Redis data through an external application

Deploy the redis-exporter application to the Container Service Kubernetes cluster to capture Redis data.

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the target cluster, and click **Dashboard** in the **Actions** column.

    ![Kubernetes cluster console button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9273229061/p61754.png)

3.  In the left-side navigation pane, choose **Workloads** \> **Deployments**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    **Note:** Change <Address\> and <Password\> to the corresponding values of Redis. You can also use the sample values provided by ARMS to experience the service:

    -   Redis address: redis://r-bp167pgqkqh7h25coypd.redis.rds.aliyuncs.com:6379
    -   Redis password: `Arms1234`
    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: redis-exporter
    spec:
      replicas: 1
      template:
        metadata:
          labels:
            app: redis-exporter
        spec:
          containers:
          - name: redis-exporter
            imagePullPolicy: Always
            env:
            - name: REDIS_ADDR
              value: "<Address>"
            - name: REDIS_PASSWORD
              value: "<Password>"
            - name: REDIS_EXPORTER_DEBUG
              value: "1"
            image: oliver006/redis_exporter
            ports:
            - containerPort: 9121
              name: redis-exporter
    ```

    In this step, the redis-exporter application is deployed to the Container Service Kubernetes cluster.

4.  In the left-side navigation pane, choose **Discovery and Load Balancing** \> **Services**. In the upper-right corner, click **CREATE**, and enter the following information in the **CREATE FROM TEXT INPUT** section:

    ```
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        app: redis-exporter
      name: redis-exporter
    spec:
      ports:
      - name: redis-exporter
        port: 9121
        protocol: TCP
        targetPort: 9121
      type: NodePort
      selector:
        app: redis-exporter
    ```


## Step 2: Configure ARMS Prometheus Monitoring to receive Redis data

Configure ARMS Prometheus Monitoring in the ARMS console to receive Redis data captured by the external application.

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
      name: redis-exporter
      # Enter the target namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # The Redis Grafana template ID is 763.
        # Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
        port: redis-exporter
        # Enter the path exposed in Prometheus Exporter code.
        path: /metrics
      namespaceSelector:
        any: true
        # The namespace of the NGINX Demo
      selector:
        matchLabels:
          # Enter the label field of service.yaml to locate the target service.yaml file.
          app: redis-exporter
    ```


## Step 3: Display the Redis data on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 763 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5248468061/p63219.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the **prom** drop-down list.

    After the configuration is complete, the ARMS Prometheus Grafana Redis dashboard is shown in the following figure.

    ![ARMS Prometheus Grafana Redis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5248468061/p63223.png)


## Step 4: Create an alert

1.  You can select one of the two available methods to go to the Create Alarm page.

    -   On the [Prometheus Grafana dashboard](http://grafana.console.aliyun.com/) page of the NewDashBoard, click And jump to the Prometheus create alarm dialog box.
    -   In the left-side navigation pane of the arms console, choose **Alarm management** \> **Alert policy management** On the alert policies page. Click **Create alarms** \> **Prometheus**.
2.  In the **create alarm** dialog box, enter all required information and click **save**.

    1.  Enter an alert name, for example, Received\_Bytes.

    2.  Select the **cluster** for which you want to create an alert.

    3.  Select **type** as the **grafana**.

    4.  Select a specific **dashboard** and **chart** to be monitored.

    5.  Configure an alert rule.

        1.  Select **meet the following rules**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of network receiving bytes \(MB\) is at least 3.

            **Note:** A Grafana chart may contain data of Curve A, Curve B, and Curve C. You can select one of them to monitor.

        3.  Edit or re-enter the PromQL statement in the **PromQL** input box.

            **Note:** An error may be reported if a PromQL statement contains a dollar sign \($\). You must delete the equal sign \(=\) and the parameters on both sides of the dollar sign \($\) from the statement that contains the dollar sign \($\). For example, to change a `folder` to a `folder`

    6.  Set Notification Mode. For example, select SMS.

    7.  Select the notification receivers. In the **all contact groups** box, click the name of a contact group. If the contact group appears in the **selected groups** box, the setting succeeds.

    ![Prometheus Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3608828061/p61774.png)


After the ARMS Prometheus Grafana Redis dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

**Related topics**  


[View Prometheus Monitoring metrics]()

[Use ARMS Prometheus Monitoring to customize Grafana dashboards]()

[Create alarms](https://www.alibabacloud.com/help/doc-detail/94833.htm)

