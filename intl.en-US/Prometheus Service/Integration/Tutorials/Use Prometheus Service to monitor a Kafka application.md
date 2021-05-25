# Use Prometheus Service to monitor a Kafka application

To monitor a Kafka application by using Prometheus Service, you must instrument the Kafka application to expose data, use Prometheus Service to capture the data, configure a Grafana dashboard to display the data, and then create an alert.

A Container Service for Kubernetes \(ACK\) cluster is connected to Prometheus Service. For more information, see [Connect an ACK cluster to Prometheus Service]().

## Procedure

The following figure shows the process of using Prometheus Service to monitor a Kafka application.

![How It Works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1253455161/p64446.png)

## Step 1: Configure the port of the JMX service

To enable the Java Management Extensions \(JMX\) service in a Kafka application to obtain resource information, perform the following steps:

1.  Add `export JMX_PORT="9999"` to the first line in the /opt/kafka/kafka\_2.11-0.8.2.1/bin/kafka-server-start.sh file.

2.  Restart the Kafka application.


## Step 2: Instrument the Kafka application

Enable jmx\_exporter to allow access to JMX information by using HTTP so that Prometheus Service can capture data.

1.  Download the [kafka.yml](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/kafka-0-8-2.yml) file to the /opt/exporter\_kafka/ directory.

2.  Add `hostPort: localhost:9999` to the first line in the downloaded /opt/exporter\_kafka/kafka-0.8.2.yml file.

    This operation exposes the port of the JMX service to jmx\_exporter.

3.  Download the [executable file](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.12.0/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar) of jmx\_exporter to the /opt/exporter\_kafka/ directory.

4.  Run the following command to enable jmx\_exporter:

    ```
    java -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.port=9998 -cp /opt/exporter_kafka/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar io.prometheus.jmx.WebServer 9997 /opt/exporter_kafka/kafka-0-8-2.yml &
    ```

    Run the following command to check whether jmx\_exporter works as expected:

    ```
    curl http://<IP address of the server where jmx_exporter is deployed>:9997/metrics
    ```

    For more information about Kafka metrics, see [Monitoring Kafka](https://docs.confluent.io/current/kafka/monitoring.html).


## Step 3: Configure Prometheus Service

To configure the Prometheus.yaml file to allow Prometheus Service to capture the data of the Kafka application, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the ACK cluster resides. Find the cluster and click **Settings** in the **Actions** column.

4.  On the Settings page, click the **Prometheus Settings** tab.

5.  On the Prometheus Settings tab, enter the following code in the Prometheus.yaml code editor and click **Save**:

    ```
    global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
    scrape_configs:
      - job_name: 'kafka'
        static_configs:
        - targets: ['121.40.XX.XX:9997']
    ```


## Step 4: Configure a Grafana dashboard

To configure a Grafana dashboard to display data, perform the following steps:

1.  Go to the [homepage of Grafana dashboards](http://g.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**.

3.  On the Import page, enter 10973, which is the ID of the Kafka Grafana template provided by Prometheus, in the **Import via grafna.com** field and click **Load** next to the field.

    ![Import Grafana Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2116394161/p61709.png)

4.  On the Import page, perform the following operations and click **Import**:

    ![Prometheus-Kafka](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7224898161/p245115.png)

    1.  Enter a dashboard name in the **Name** field.

    2.  Select your ACK cluster from the **Folder** drop-down list.

    3.  Select your ACK cluster from the **Select a Prometheus data source** drop-down list.

    The following figure shows the configured Grafana dashboard.

    ![prometheus_kafka_grafana](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7088468061/p63693.png)


## Step 5: Create an alert

To create an alert to monitor metrics of Prometheus Service, perform the following steps:

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


