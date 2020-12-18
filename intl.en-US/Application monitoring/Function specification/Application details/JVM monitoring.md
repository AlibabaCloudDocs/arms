# JVM monitoring

The application monitoring function of Application Real-Time Monitoring Service \(ARMS\) provides the Java Virtual Machine \(JVM\) monitoring function. It monitors heap metrics, non-heap metrics, direct buffer metrics, memory-mapped buffer metrics, garbage collection \(GC\) details, and the number of JVM threads. This topic describes the JVM monitoring feature and how to monitor JVM metrics.

## Features

ARMS' JVM monitoring feature can help you monitor the following metrics.

-   Heap memory
    -   heap\_init: initial bytes of the heap memory
    -   heap\_max: maximum bytes of the heap memory
    -   heap\_commited: submitted bytes of the heap memory
    -   heap\_used: used bytes of the heap memory
-   Non-heap memory
    -   non\_heap\_init: initial bytes of the non-heap memory
    -   non\_heap\_max: maximum bytes of the non-heap memory
    -   non\_heap\_commited: submitted bytes of the non-heap memory
    -   non\_heap\_used: used bytes of the non-heap memory
-   Direct buffer
    -   direct\_capacity: total size of direct buffer \(in bytes\)
    -   direct\_used: used size of the direct buffer \(in bytes\)
-   Memory-mapped buffer
    -   mapped\_capacity: total size of memory-mapped buffer \(in bytes\)
    -   mapped\_used: used size of memory-mapped buffer \(in bytes\)
-   GC details
    -   GcPsMarkSweepCount: GC Parallel Scavenge MarkSweep amount
    -   GcPsScavengeCount: GC Parallel Scavenge amount
    -   GcPsMarkSweepTime: GC Parallel Scavenge MarkSweep time
    -   GcPsScavengeTime: GC Parallel Scavenge time
-   Number of JVM threads
    -   ThreadCount: total number of threads
    -   ThreadDeadLockCount: number of deadlocked threads
    -   ThreadNewCount: number of new threads
    -   ThreadBlockedCount: number of blocked threads
    -   ThreadRunnableCount: number of treads that can run
    -   ThreadTerminatedCount: number of terminated threads
    -   ThreadTimedWaitCount: number of threads in timed waiting
    -   ThreadWaitCount: number of waiting threads

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page, click the name of the target application.

3.  On the Application Details page, select the target node and click the **JVM Monitoring** tab on the right side of the page.

    The JVM Monitoring tab shows the time sequence curves of the instantaneous times of GC, instantaneous time consumption of GC, heap memory details, non-heap memory details, and number of JVM threads.

    -   Click **Instantaneous** and **Accumulated** in the upper-right corner of **Instantaneous Count/Min** and **Instantaneous Duration/Min** panels. You can alternatively view the time sequence curves of the instantaneous or accumulated times and time consumption of GC. By default, the instantaneous values are displayed.
    -   Click a metric name \(for example, the number of instantaneous GC times\) on each monitoring panel to enable or disable the visibility of this metric in the chart.

        **Note:** Each chart must have at least one visible metric.


