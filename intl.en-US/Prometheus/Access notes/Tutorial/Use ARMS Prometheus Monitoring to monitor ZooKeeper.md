# Use ARMS Prometheus Monitoring to monitor ZooKeeper

This tutorial describes how to expose data by using instrumentation points in ZooKeeper, capture data by using Create a Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\), and display data on the ARMS Prometheus Grafana dashboard, to ultimately monitor ZooKeeper with ARMS Prometheus Monitoring.

## Step 1: Start the JMX service

Enable the Java Management Extensions \(JMX\) service in ZooKeeper to acquire resource information.

1.  Add `JMXPORT=8999` in line 44 in the /opt/zk/zookeeper-3.4.10/bin/zkServer.sh file as follows:

    ```
    if [ "x$JMXLOCALONLY" = "x" ]
    then
        JMXLOCALONLY=false
    fi
    
    JMXPORT=8999 ## Added here in line 44
    
    if [ "x$JMXDISABLE" = "x" ] || [ "$JMXDISABLE" = 'false' ]
    then
      echo "ZooKeeper JMX enabled by default $JMXPORT ..." >&2
      if [ "x$JMXPORT" = "x" ]
      then
    ```

2.  Restart ZooKeeper.

    ```
    /opt/zk/zookeeper-3.4.10/bin/zkServer.sh start /opt/zk/zookeeper-3.4.10/conf/zoo_sample.cfg &
    ```


## Step 2: Start jmx\_exporter in ZooKeeper

Start jmx\_exporter to allow access to JMX information through HTTP so that ARMS Prometheus Monitoring can capture data.

1.  Download [zookeeper.yaml](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/zookeeper.yaml) to the /opt/exporter\_zookeeper/ directory.

2.  Add `hostPort: localhost:8999` to the first line in the downloaded file /opt/exporter\_zookeeper/zookeeper.yaml to expose the running port of the JMX service to jmx\_exporter.

3.  Download the [executable file](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/0.12.0/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar) of jmx\_exporter to the opt/exporter\_zookeeper/ directory.

4.  Start jmx\_exporter.

    ```
    java -Dcom.sun.management.jmxremote.ssl=false -
    Dcom.sun.management.jmxremote.authenticate=false -
    Dcom.sun.management.jmxremote.port=8998 -cp /opt/exporter_zookeeper/jmx_prometheus_httpserver-0.12.0-jar-with-dependencies.jar 
    io.prometheus.jmx.WebServer 8997 /opt/exporter_zookeeper/zookeeper_exporter.yaml &
    ```

    The application configuration is complete. You can run the following command to check whether jmx\_exporter is running properly:

    ```
    curl http://<IP address of the server where jmx_exporter is located>:9997/metrics
    ```


## Step 3: Configure ARMS Prometheus Monitoring to capture the data of ZooKeeper

Configure ARMS Prometheus Monitoring in the ARMS console to capture the data of ZooKeeper.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the top of the **Prometheus monitoring** page, select the region where the Container Service Kubernetes cluster is located, and click the name of the target cluster.

4.  On the page that appears, click the **Details** tab and then click **Edit prometheus.yaml**.

5.  Paste the following code to the file.

    ```
      global:
      scrape_interval:     15s # Set the scrape interval to every 15 seconds. 
    Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
    scrape_configs:
      - job_name: 'zookeeper'    
        static_configs:    
        - targets: ['121.40.124.46:8997']
    ```


## Step 4: Display ZooKeeper data on the Grafana dashboard

Import the Grafana dashboard template in the ARMS console and specify the Container Service Kubernetes cluster where the Prometheus data source is located.

1.  Go to [Host Dashboard](http://grafana.console.aliyun.com/).

2.  In the left-side navigation pane, choose **+** \> **Import**, enter 10981 in the **Grafana.com Dashboard** field, and click **Load**.

    ![Import Grafana dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6969283851/p61709.png)

3.  On the Import page, set the following information and click **Import**.

    ![Import Grafana dashboard with options](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8798468061/p64454.png)

    1.  Enter a custom dashboard name in the **Name** field.

    2.  Select your Container Service Kubernetes cluster from the **Folder** drop-down list.

    3.  Select your Container Service Kubernetes cluster from the drop-down list at the bottom.

    After the configuration is complete, the ARMS Prometheus Grafana ZooKeeper dashboard appears, as shown in the following figure.

    ![prom-zoo gra](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8798468061/p63907.png)


## Step 5: Create an alert

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


After the ARMS Prometheus Grafana ZooKeeper dashboard is configured, you can view Prometheus Monitoring metrics and customize the dashboard. For more information, see the following documents.

**Related topics**  


[View the metrics of Prometheus Service]()

[Use Alibaba Cloud Prometheus to customize the Grafana dashboard]()

[Create alarms](https://www.alibabacloud.com/help/doc-detail/94833.htm)

