# JVM monitoring

The Java Virtual Machine \(JVM\) monitoring feature is used to monitor important JVM metrics, such as heap memory, non-heap memory, direct buffer, memory-mapped buffer, garbage collection \(GC\) details, and the number of JVM threads. This topic describes the JVM monitoring feature and how to monitor JVM metrics.

## Features

The JVM monitoring feature can help you monitor the following metrics:

-   Instantaneous and accumulated GC statistics
    -   FullGC Count
    -   YoungGC Count
    -   FullGC Duration
    -   YoungGC Duration
-   Heap Memory Details
    -   Total
    -   Old Generation
    -   Survivor Space of Young Generation
    -   Eden Space of Young Generation
-   Non-Heap Memory
    -   Non Heap Committed
    -   Non Heap Init
    -   Non Heap Max
-   Metaspace Details
    -   Metaspace
-   Direct Buffer
    -   Direct Capacity
    -   Direct Used
-   JVM Threads
    -   Thread Count
    -   Thread Dead Lock Count
    -   Thread New Count
    -   Thread Blocked Count
    -   Thread Runnable Count
    -   Thread Terminated Count
    -   Thread Time Wait Count
    -   Thread Wait Count

![Application Monitoring > Application Details > JVM Monitoring](../images/p43130.png "JVM monitoring")

## View JVM metrics

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, click the application that you want to view.
3.  In the left-side navigation pane, choose Application Monitoring \> Application Details. On the page that appears, click the node that you want to view, and then click the **JVM Monitoring** tab on the right side.

    On the JVM Monitoring tab, view the time sequence curves of the instantaneous GC count, instantaneous GC duration, heap memory details, non-heap memory details, and number of JVM threads.

    -   Click **Instantaneous** and **Accumulated** in the upper-right corner of the **Instantaneous Count / 1 Min** and **Instantaneous Duration / 1 Min** panels to view the time sequence curves of the instantaneous and accumulated GC times and GC duration. By default, the instantaneous GC times and duration are displayed.
    -   Click a metric name such as FullGC Count or YoungGC Count on a monitoring panel to enable or disable the visibility of this metric.

        **Note:** Each chart must contain at least one visible metric. When there is only one metric in the chart, you cannot turn off its visibility.


