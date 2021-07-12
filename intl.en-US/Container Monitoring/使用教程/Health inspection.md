# Health inspection

The health inspection feature can be used to periodically test the connectivity of your monitored services. This feature allows you to know the health status of the monitored services, and detect and handle exceptions at the earliest opportunity. You can quickly create ACK Service inspections by importing ACK Service data for container monitoring in batches.

Your service is connected to container monitoring. For more information, see [Enable container monitoring]().

## Create an ACK service inspection task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Container Monitoring**.

3.  In the top navigation bar, select the region where your instance is located.

4.  Log on to the **Container monitoring**On the page that appears, click the name of the Kubernetes cluster.

5.  In the left-side navigation pane, choose **Health inspection**.

6.  Log on to the **Inspection**In the upper-right corner of the tab, click **ACK Service inspection**.

7.  Log on to the **New health inspection for ACK Service \(TCP\)**In the dialog box, select the ACK Service data to be imported, and then click **Determine**.

    **Note:** The ACK service inspection feature supports the following inspection types:

    -   Internal endpoints: TCP and Ping
    -   External endpoints: TCP, Ping, and HTTP

## Create other types of inspections

Health inspectionYou can also create custom inspections and cloud service inspections:

-   For the operation of creating a custom inspection, see [Custom inspection]().
-   For operations on creating cloud service inspections, see [Alibaba Cloud service inspection]().

