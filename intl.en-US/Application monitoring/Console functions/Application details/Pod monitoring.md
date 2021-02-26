# Pod monitoring

This topic shows you how to view the monitored metrics of a pod, including the metrics of CPU, physical memory, network traffic, and network packets.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

**Note:** Pod metrics are available only for applications that are deployed in pods.

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select a pod where the application is deployed, set the time period, and then click the **Pod Monitoring** tab.

    ![Pod Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4415424161/p236424.png)


## CPU

The **CPU** section displays the CPU metrics of the pod where the application is deployed in the specified time period, including the following metrics:

-   Cumulative CPU usage
-   CPU quota

![CPU](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4415424161/p236432.png)

1.  In the **CPU** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click legend to hide or show the data.

## Physical memory

The **Memory** section displays the physical memory metrics of the pod where the application is deployed in the specified time period, including the following metrics:

-   Memory usage
-   Memory quota

![Memory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4415424161/p236434.png)

1.  In the **Memory** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click legend to hide or show the data.

## Network traffic

The **Network Traffic** section displays the network traffic metrics of the pod where the application is deployed in the specified time period, including the following metrics:

-   Received network traffic \(bytes\)
-   Sent network traffic \(bytes\)

![Network Traffic](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4415424161/p236437.png)

1.  In the **Network Traffic** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click legend to hide or show the data.

## Network packets

The **Network Packets** section displays the network packet metrics of the pod where the application is deployed in the specified time period, including the following metrics:

-   Number of discarded network packets among the sent network packets
-   Number of sent network packets
-   Number of discarded network packets among the received network packets
-   Number of errors that occur when network packets are sent
-   Number of errors that occur when network packets are received

![Network Packets](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4415424161/p236441.png)

1.  In the **Network Packets** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click legend to hide or show the data.

