# Use Prometheus Service to monitor a Redis database

To monitor a Redis database, you can use Prometheus Service to capture Redis data, configure a Grafana dashboard to display the captured data, and then create an alert. This topic describes how to use Prometheus Service to monitor a Redis database. In this example, Container Service for Kubernetes \(ACK\) and Container Registry are also used.

An ACK cluster is connected to Prometheus Service. For more information, see [Connect an ACK cluster to Prometheus Service]().

## Procedure

The following figure shows the process of using Prometheus Service to monitor a Redis database.

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4116155161/p149087.png)

## Step 1: Deploy an application

To deploy the redis-exporter image to an ACK cluster to capture Redis data, perform the following steps:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, find the cluster to which you want to deploy the image and click **Applications** in the **Actions** column.

4.  Create a container group.

    1.  In the left-side navigation pane, choose **Workloads** \> **Deployments**.

    2.  On the **Deployments** page, click **Create from YAML** in the upper-right corner.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

        **Note:** Replace <Address\> and <Password\> with the corresponding values of the Redis database. You can also use the following sample values that are provided by Application Real-Time Monitoring Service \(ARMS\):

        -   Redis address: redis://r-bp167pgqkqh7h25coypd.redis.rds.aliyuncs.com:6379
        -   Redis password: Arms1234
        ```
        apiVersion: apps/v1 # for versions before 1.8.0 use apps/v1beta1
        kind: Deployment
        metadata:
          name: redis-exporter
          labels:
            app: redis-exporter
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: redis-exporter
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

    The **Deployments** page displays the created container group.

    ![redis-exporter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6493898161/p249085.png)

5.  Create a service.

    1.  In the left-side navigation pane, choose **Services and Ingresses** \> **Services**.

    2.  On the **Services** page, click **Create Resources in YAML**.

    3.  On the **Create** page, enter the following code in the **Template** code editor and click **Create**:

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

    The **Services** page displays the created service.

    ![redis-exporter service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7705419161/p249091.png)


## Step 2: Configure service discovery

To configure service discovery of Prometheus Service to receive data from the Redis database, perform the following steps:

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
      name: redis-exporter
      # Enter a namespace.
      namespace: default
    spec:
      endpoints:
      - interval: 30s
        # The Redis Grafana template ID is 763.
        # Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
        port: redis-exporter
        # Enter the value of the Path field for Prometheus Exporter.
        path: /metrics
      namespaceSelector:
        any: true
        # The namespace of demo.
        matchLabels:
          # Enter the value of the Label field in the service.yaml file to find the service.yaml file.
          app: redis-exporter
    ```

    The **ServiceMonitor** tab displays the configured service discovery task.

    ![Redis service discovery](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7493898161/p249103.png)


## Step 3: Configure a Grafana dashboard

To configure a Grafana dashboard to display data, perform the following steps:

1.  Go to the [homepage of Grafana dashboards](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**.

3.  On the Import page, enter 763, which is the ID of the Redis Grafana template provided by Prometheus, in the **Import via grafna.com** field and click **Load** next to the field.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2116394161/p61709.png)

4.  On the Import page, perform the following operations and click **Import**:

    ![Import Grafana Dashboard with Options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9116394161/p63219.png)

    1.  Enter a dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **prom** drop-down list.

    The following figure shows the configured Grafana dashboard.

    ![ARMS Prometheus Grafana Redis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5248468061/p63223.png)


## Step 4: Create an alert

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


