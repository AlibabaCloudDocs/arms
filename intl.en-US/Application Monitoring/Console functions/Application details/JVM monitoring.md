# JVM monitoring

The Java Virtual Machine \(JVM\) monitoring feature allows you to monitor key JVM metrics, including the metrics related to the heap memory, non-heap memory, direct buffer, memory-mapped buffer, garbage collections \(GCs\), and JVM threads. This topic describes the JVM monitoring feature and shows you how to view the JVM metrics.

## Go to the JVM monitoring tab

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

3.  On the Applications page, click the name of the application that you want to manage.

4.  In the left-side navigation pane, click **Application Details**.

5.  On the **Application Details** page, click the instance that you want to view in the left-side pane, and then click the **JVM monitoring** tab on the right side.

    ![JVM monitoring - ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9617078061/p143547.png)


## View the JVM metrics

On the **JVM monitoring** tab, you can view the time series curves for the instantaneous GC count, instantaneous GC time consumption, heap memory details, metadata details, non-heap memory details, direct buffer details, and JVM thread count.

-   You can click **Instantaneous** or **Accumulated** in the upper-right corner of the **Instantaneous Count / 1 Min** and **Instantaneous Duration / 1 Min** charts to switch between different curves. You can view the time series curves for the instantaneous GC count, accumulated GC count, instantaneous GC time consumption, and accumulated GC time consumption.
-   You can click the name of a metric such as FullGC Count on a chart to show or hide the metric.

    **Note:** Each chart must contain at least one visible metric. Therefore, if only one metric is displayed in a chart, you cannot hide this metric.

-   You can click the View API icon in the upper-right corner of the **Heap Memory Details / 1 Min**, **Metadata Details / 1 Min**, **Non-Heap Memory / 1 Min**, **Direct Buffer / 1 Min**, and **JVM Threads / 1 Min** charts to view the detailed information about the APIs that are related to the metrics.

## Metrics

The JVM monitoring feature can be used to monitor the following metrics:

-   Instantaneous and accumulated GC details
    -   Number of full heap GCs \(Full GCs\)
    -   Number of GCs in the young generation
    -   Time consumed for Full GCs
    -   Time consumed for GCs in the young generation
-   Heap memory details
    -   Total heap memory
    -   Bytes of the heap memory in the old generation
    -   Bytes of the heap memory in the young generation \(survivor space\)
    -   Bytes of the heap memory in the young generation \(eden space\)
-   Non-heap memory details
    -   Submitted bytes of the non-heap memory
    -   Initial bytes of the non-heap memory
    -   Maximum bytes of the non-heap memory
-   Metaspace details

    Bytes of metaspace

-   Direct buffer details
    -   Total bytes of the direct buffer
    -   Used bytes of the direct buffer
-   JVM thread details
    -   Total number of threads
    -   Number of deadlocked threads
    -   Number of new threads
    -   Number of blocked threads
    -   Number of runnable threads
    -   Number of terminated threads
    -   Number of threads in the timed waiting state
    -   Number of waiting threads

