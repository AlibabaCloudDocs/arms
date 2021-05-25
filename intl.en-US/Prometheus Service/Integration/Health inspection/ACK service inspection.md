# ACK service inspection

The health inspection feature can be used to periodically test the connectivity of your monitored services. This feature allows you to check the health status of the monitored services and handle detected exceptions at the earliest opportunity. You can import the service data of Container Service for Kubernetes \(ACK\) that is collected by Prometheus Service to create an inspection task for the ACK services.

The services that you want to monitor are connected to Prometheus Service. For more information, see [Access to Alibaba Cloud Prometheus Service]().

## Create an ACK service inspection task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar, select a region.

4.  On the **Prometheus Monitoring** page, click the name of a Kubernetes cluster.

5.  In the left-side navigation pane, click **Health inspection**.

6.  In the upper-right corner of the **Health inspection** page, click **ACK Inspection**.

7.  In the **Create ACK Inspection** dialog box, select the ACK data that you want to import and click **OK**.

    **Note:** The ACK service inspection feature supports the following inspection types:

    -   Internal endpoints: TCP and Ping
    -   External endpoints: TCP, Ping, and HTTP

