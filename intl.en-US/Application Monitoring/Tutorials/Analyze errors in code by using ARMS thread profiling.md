# Analyze errors in code by using ARMS thread profiling

Application Real-Time Monitoring Service \(ARMS\) thread profiling is a code-level diagnostics feature. It can automatically capture stack snapshots of slow calls and reproduce the code execution process.

## Scenarios

-   ARMS thread profiling can find out problematic code with efficiency during periods of high traffic such as sales events.
-   If large numbers of slow calls occur in the system, ARMS thread profiling can automatically save the first scene.
-   If occasional slow calls cannot recur because the business is too complex, ARMS thread profiling can reproduce the code execution process.

## Set thread profiling parameters

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the Applications page, select a region in the top navigation bar.
3.  On the Applications page, click the name of the application that you want to manage.
4.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.
5.  In the **Thread settings** section, turn on or turn off Thread profiling total control switch and set the Slow call listen trigger threshold parameter.

    **Note:**

    -   The listener starts only when the response time of a service call exceeds the threshold, which is 2,000 ms by default. The listening lasts until the call ends or the consumed time exceeds 15s.

    -   We recommend that you set the threshold to the 99th percentile of the call response time. For example, if 100 calls are listed in ascending order by response time, the time consumed by the 99th one is the 99th percentile.

    ![Thread settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5331468061/p42294.png)


## View thread profiling details by using API snapshots

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the Applications page, select a region in the top navigation bar.
2.  On the Applications page, click the name of the application that you want to manage.
3.  In the left-side navigation pane, click **Interface Invocation**. On the page that appears, select the required API and click the **Interface Snapshot** tab.
4.  On the Interface Snapshot tab, click the required trace ID.

    The Traces tab appears.

5.  In the **Details** column, click the magnifier icon.

    The Details pane appears.

    ![Thread analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7673658061/p42295.png)

    **Note:**

    -   The actual response time is the amount of time a service call consumes and is not affected by thread profiling.

    -   The listening response time is the amount of time when thread profiling is effective. Typically, the listening response time is approximately the actual response time minus the listening threshold for slow calls.


## View thread profiling details by using a trace query

1.  In the left-side navigation pane of the console, choose **Application Monitoring** \> **Invocation Trace Query**.
2.  In the **Parameter type** drop-down list of the Call link query page, select **Only thread profiling snapshots are included** and click **Add to query criteria**.

    ![Thread profiling snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7673658061/p180552.png)

3.  In the query result, click the required trace ID.

    The Traces tab appears.

4.  In the **Thread Profiling** column, click the magnifier icon.

    The Thread Profiling dialog box appears.


## FAQ

-   Q: What is the actual response time?

    A: The actual response time is the amount of time a service call consumes and is not affected by thread profiling.

-   Q: What is the listening response time?

    A: The listening response time is the amount of time when thread profiling is effective. To minimize listening pressure, thread profiling listens only to the range of execution time that exceeds the listening threshold of slow calls. The default threshold is 2s. If a slow call consumes 5s, thread profiling listens to only the time range between the third and fifth second. If a call consumes 1.8s, thread profiling does not listen to the call.

-   Q: Why is the listening response time shorter than the actual response time? Why does the listener miss some slow calls that exceed the listening threshold?

    A:

    -   Thread profiling listens only to the range of execution time that exceeds the listening threshold of slow calls. Typically, the listening response time is approximately the actual response time minus the listening threshold for slow calls.
    -   If the system has a large number of slow calls at the same time, the listener may miss specific slow calls after the listening threshold is exceeded because the number of listening threads is limited. In this case, the listening response time is shorter than the actual response time and the listener may miss calls.
    -   To ensure that slow calls that exceed 5s are listened to, thread profiling configures independent listening threads for these slow calls. In this case, the listening response time is approximately the actual response time minus 5s.

