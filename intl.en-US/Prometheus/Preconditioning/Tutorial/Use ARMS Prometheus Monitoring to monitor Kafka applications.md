# Use ARMS Prometheus Monitoring to monitor Kafka applications

This tutorial describes how to expose data by using instrumentation points in Kafka applications, capture data by using Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\), and display data on the ARMS Prometheus Grafana dashboard, to ultimately monitor Kafka applications with ARMS Prometheus Monitoring.

The following figure shows the workflow.

![How it works](../images/p64446.png)

## Step 1: Start the JMX service

Enable the Java Management Extensions \(JMX\) service in Kafka applications to acquire resource information.

1.  Add `export JMX_PORT="9999"` to the first line in the /opt/kafka/kafka\_2.11-0.8.2.1/bin/kafka-server-start.sh file.

2.  Restart Kafka.


## Step 2: Start jmx\_exporter

Start jmx\_exporter to allow access to JMX information through HTTP so that ARMS Prometheus Monitoring can capture data.

1.  Download the [kafka.yml](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/kafka-0-8-2.yml) file to the /opt/exporter\_kafka/ directory.

2.  Modify the downloaded file /opt/exporter\_kafka/kafka-0.8.2.yml by adding `hostPort: localhost:9999` to the first line in the file to expose the running port of the JMX service to jmx\_exporter.

3.  Download the [executable file](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.12.0/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar) of jmx\_exporter to the /opt/exporter\_kafka/ directory.

4.  Start jmx\_exporter.

    ```
    java -Dcom.sun.management.jmxremote.ssl=false -
    Dcom.sun.management.jmxremote.authenticate=false -
    Dcom.sun.management.jmxremote.port=9998 -cp 
    /opt/exporter_kafka/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar 
    io.prometheus.jmx.WebServer 9997 /opt/exporter_kafka/kafka-0-8-2.yml &
    ```

    The application configuration is complete. You can run the following command to check whether jmx\_exporter is running properly:

    ```
    curl http://<IP address of the server where jmx_exporter is located>:9997/metrics
    ```

    For more information about Kafka metrics, see [Monitoring Kafka](https://docs.confluent.io/current/kafka/monitoring.html).


## Step 3: Configure ARMS Prometheus Monitoring to capture the data of Kafka applications

Configure ARMS Prometheus Monitoring in the ARMS console to capture the data of Kafka applications.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located, and click the name of the target cluster.

4.  On the page that appears, click the **Details** tab and then click **Edit prometheus.yaml**.

    ![prom_kafka yaml](../images/p63677.png)

5.  Paste the following code to the file.

    ```
      global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
      scrape_configs:
      - job_name: 'kafka'
        static_configs:
        - targets: ['121.40.124.46:9997']
    ```


## Step 4: Display the data of Kafka applications on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 10973 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](../images/p63196.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the **prometheus-apl** drop-down list.

    After the configuration is complete, the ARMS Prometheus Grafana Kafka dashboard appears, as shown in the following figure.

    ![prometheus_kafka_grafana](../images/p63693.png)


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


After the ARMS Prometheus Grafana Kafka dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

[View the metrics of Prometheus Service]()

[Use ARMS Prometheus Monitoring to customize the Grafana dashboard]()

[Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md)

**Related topics**  


[What is Prometheus Service?]()

