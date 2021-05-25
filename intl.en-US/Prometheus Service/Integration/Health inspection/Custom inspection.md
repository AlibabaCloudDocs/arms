# Custom inspection

The health inspection feature can be used to periodically test the connectivity of your monitored services. This feature allows you to check the health status of the monitored services and handle detected exceptions at the earliest opportunity. You can create a custom health inspection task for a specified service.

The services that you want to monitor are connected to Prometheus Service. For more information, see [Access to Alibaba Cloud Prometheus Service]().

## Create a custom inspection task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar, select a region.

4.  On the **Prometheus Monitoring** page, click the name of a Kubernetes cluster.

5.  In the left-side navigation pane, click **Health inspection**.

6.  In the upper-right corner of the **Health inspection** page, click **Create inspection**.

7.  In the **Create inspection** dialog box, configure the parameters, click **Link test** to test the connectivity, and then click **OK**.

    ![Create an inspection task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8548342161/p232683.png)

    |Parameter|Description|
    |---------|-----------|
    |Checkpoint|The checkpoint of the inspection task. Enter an IP address or a domain name. For example, you can set the value to 11.113.2.1 or www.aliyun.com.|
    |Inspection Type|The type of the inspection task.     -   HTTP
    -   Ping
    -   HTTPS
    -   TCP |
    |Frequency|The interval at which the inspection task is run. Valid values:     -   Every 10s
    -   Every 30s
    -   Every 60s
    -   Every 120s |


