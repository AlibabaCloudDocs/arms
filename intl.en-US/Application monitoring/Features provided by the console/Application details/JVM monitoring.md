# JVM monitoring

The Java Virtual Machine \(JVM\) monitoring feature allows you to monitor critical JVM metrics. The critical metrics include heap metrics, non-heap metrics, direct buffer metrics, memory-mapped buffer metrics, garbage collection \(GC\) details, and JVM thread count. This topic describes the JVM monitoring feature and how to monitor JVM metrics.

![JVM monitoring-ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9617078061/p143547.png)

## Features

The JVM monitoring feature allows you to monitor the following metrics:

-   Instantaneous and accumulated GC details
    -   Total times of GC
    -   Times of young GC
    -   Total time consumption of GC
    -   Time consumption of young GC
-   Heap memory details
    -   Total heap memory
    -   Bytes of old heap memory
    -   Bytes of young heap memory \(Survivor\)
    -   Bytes of young heap memory \(Eden\)
-   Non-heap memory
    -   Submitted bytes of the non-heap memory
    -   Initial bytes of the non-heap memory
    -   Maximum bytes of the non-heap memory
-   Metaspace

    Bytes of metaspace

-   Direct buffer
    -   Total bytes of direct buffer
    -   Used bytes of direct buffer
-   Number of JVM threads
    -   Total number of threads
    -   Number of deadlocked threads
    -   Number of new threads
    -   Number of blocked threads
    -   Number of runnable threads
    -   Number of terminated threads
    -   Number of threads in timed waiting
    -   Number of waiting threads

## View JVM metrics

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. At the top of the Applications page, select a region.

3.  On the Applications page, click the application that you want to view.

4.  In the left-side navigation pane, click **Application Details**.

5.  On the **Application Details** page, select the node and click **JVM monitoring** tab on the right side of the page.

    On the **JVM monitoring** tab, the time sequence curves of the instantaneous GC count, instantaneous GC duration, heap memory details, metadata details, non-heap memory details, direct buffer, and JVM threads are displayed.

    -   Click **Instantaneous** and **Accumulated** in the upper-right corner of **Instantaneous Count / 1 Min** and **Instantaneous Duration / 1 Min** panels. You can view the time sequence curves of the instantaneous GC count or accumulated GC count. You can also view the time sequence curves of instantaneous GC duration.
    -   Click a metric name \(for example, the total times of GC\) on a monitoring panel to enable or disable the visibility of the metric in the chart.

        **Note:** Each chart must contain at least one visible metric. If only one metric is displayed in the chart, you cannot disable the visibility of the metric.

    -   Click View API in the upper-right corner of **Heap Memory Details / 1 Min**, **Metadata Details / 1 Min**, **Non-Heap Memory / 1 Min**, **Direct Buffer / 1 Min**, and **JVM Threads / 1 Min** panels to view the API details of the monitoring metric.

