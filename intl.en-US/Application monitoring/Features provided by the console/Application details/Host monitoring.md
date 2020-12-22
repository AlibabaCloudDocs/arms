---
keyword: [ARMS, EDAS, Host, Monitoring]
---

# Host monitoring

The host monitoring feature is used to monitor the metrics of CPU, memory, disk, load, network traffic, and network packets. This topic describes the host monitoring feature and how to view host monitoring metrics.

![Application Monitoring > Application Details > HOST Monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1117358061/p43131.png)

## Features

The host monitoring feature can monitor the following metrics:

-   CPU
    -   Total CPU usage
    -   System CPU usage
    -   User CPU usage
    -   Usage of CPU waiting for I/O
-   Memory
    -   Total memory
    -   Free memory
    -   Used memory
    -   Memory in PageCache
    -   Memory in BufferCache
-   Disk
    -   Total disk space \(bytes\)
    -   Free disk space \(bytes\)
    -   Used disk space \(bytes\)
-   Load

    System load

-   Network traffic
    -   Received network traffic \(bytes\)
    -   Sent network traffic \(bytes\)
-   Network packets
    -   Received packets per minute
    -   Sent packets per minute
    -   Received errors per minute
    -   Discarded packets per minute

## View host monitoring metrics

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.
3.  On the Applications page, click the application that you want to monitor.
4.  In the left-side navigation pane, click **Application Details**.
5.  On the Application Details page, click the node that you want to view, and then click the **HOST Monitoring** tab on the right side.

    On the HOST Monitoring tab, you can view the time sequence curves of metrics including CPU, memory, disk, load, network traffic, and network packets.

    -   You can click the name of a metric such as cpu\_sys on each monitoring panel to toggle the visibility of this metric.

        **Note:** Each chart must contain at least one visible metric. Therefore, if only one metric is displayed on a monitoring panel, it cannot be set to invisible.

    -   You can click the line chart icon in the upper-right corner to view the metrics by range or compare the metrics.
    -   You can click the View API icon in the upper-right corner to view the detailed information about the API operations related to the metric.
    -   You can click the or icon in the upper-right corner of the monitoring panel to create an alert or view the existing alert points. For more information about how to create an alert, see [Create an alert](https://www.alibabacloud.com/help/doc-detail/94833.htm).

