# Analyze errors in code by using ARMS thread profiling

Application Real-Time Monitoring Service \(ARMS\) thread profiling is a code-level diagnosis tool. It can automatically capture stack snapshots of slow calls and restore the code execution process.

## Scenario

-   ARMS thread profiling can quickly locate problematic code during periods of high traffic such as sales events.
-   If large amounts of slow calls occur in the system, ARMS thread profiling can automatically save the first scene.
-   If occasional slow calls cannot recur because the business is too complex, ARMS thread profiling can restore the real code execution process.

## Set thread profiling parameters

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.
3.  On the Applications page, click the name of the application.
4.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.
5.  In the **Thread Settings** section, you can turn on or turn off the thread profiling total control switch and set the slow call listen trigger threshold.

    **Note:**

    -   The listener starts only when the service call response time exceeds the threshold \(2,000 ms by default\) and it lasts until the call ends or the consumed time exceeds 15 seconds.

    -   We recommend that you set the threshold to the 99th percentile of the call response time. For example, if 100 calls are listed in ascending order by response time, the time consumed by the 99th one is the 99th percentile.

    ![Thread settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7563658061/p42294.png)


## View thread profiling details by using interface snapshots

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.
2.  On the Applications page, click the name of the application.
3.  In the left-side navigation pane, click **Interface Invocation**, select the interface on the right side of the page, and click the **Interface Snapshot** tab.
4.  On the Interface Snapshot tab, click a TraceId link.

    The Traces tab appears.

5.  In the **Thread Profiling** column, click the magnifier icon.

    The Thread Profiling dialog box appears.

    ![Thread analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7673658061/p42295.png)

    **Note:**

    -   The actual response time is the amount of time it takes for the service call to execute and is not affected by thread profiling.

    -   The listening response time is the amount of time consumed by thread profiling. Typically, the listening response time is approximately the actual response time minus the listening threshold for slow calls.


## View thread profiling details by using trace query

1.  In the left-side navigation pane of the console, choose **Application Monitoring** \> **Invocation Trace Query**.
2.  In the **Parameter Name** drop-down list of the Invocation Trace Query tab, select **Only thread profiling snapshots are included.** and click **Search**.

    ![Thread profiling snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7673658061/p180552.png)

3.  Click a TraceId link in the search results.

    The Traces tab appears.

4.  In the **Thread Profiling** column, click the magnifier icon.

    The Thread Profiling dialog box appears.


## FAQ

-   Q: What is the actual response time?

    A: The actual response time is the amount of time it takes for the service call to execute and is not affected by thread profiling.

-   Q: What is the listening response time?

    A: The listening response time is the amount of call execution time consumed by thread profiling. To minimize listening pressure, thread profiling listens only for the execution time that exceeds the listening threshold of slow calls. The default threshold is 2 seconds. For example, assume that thread profiling listens for a slow call that consumes 5 seconds and only listens to the interval between 3 and 5 seconds. If a call consumes 1.8 seconds, the listener does not listen to the call.

-   Q: Why is the listening response time shorter than the actual response time? Why does the listener miss some slow calls that exceed the listening threshold?

    A:

    -   Thread profiling listens only for the execution time of a call after the listening threshold is exceeded. Typically, the listening response time is approximately the actual response time minus the listening threshold for slow calls.
    -   If the system has a large number of slow calls at the same time, the listener may miss some slow calls after the listening threshold is triggered because the number of listening threads is limited. In this case, the listening response time is shorter than the actual response time and the listener may miss the calls.
    -   To ensure that slow calls that exceed five seconds are listened, thread profiling configures independent listening threads for these slow calls. In this case, the listening response time is approximately the actual response time minus five seconds.

