# Use ARMS TProf to analyze code problems

Application Real-Time Monitoring Service \(ARMS\) TProf is a code-based diagnosis tool. It can automatically capture stack snapshots of slow calls and truly restore the first scene of code execution.

## Scenarios

Here are typical scenarios of the use of ARMS TProf:

-   If slow calls occur during the peak traffic of promotions and sales, ARMS TProf can help you quickly locate the faulty code.

-   If large amounts of slow calls occur in the system, ARMS TProf can automatically save the first scene.

-   If occasional slow calls cannot recur because the business is too complex, ARMS TProf can restore the real code execution trajectory.


## Procedure

**Set thread profiling parameters**

1.  In the left-side navigation pane of the console, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, click the name of the target application.

3.  In the left-side navigation pane, click **Application Setup** and then the Custom Configuration tab on the right of the page.

4.  In the **Thread Profiling Settings** section, you can turn the thread profiling control switch on or off, and set the trigger threshold for slow calls.

**Note:**

-   The listener is started only when the service call response time exceeds the threshold \(1,000 ms by default\), and it lasts until the call ends or the consumed time exceeds 15 seconds.

-   We recommend that you set the threshold to the 99th percentile of the call response time For example, if 100 calls are listed in ascending order by response time, the 99th one is represented by the 99th percentile.


**View thread profiling details through interface snapshots**

1.  In the left-side navigation pane of the console, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, click the name of the target application.

3.  In the left-side navigation pane, click **Interface Invocation**, and then the **Interface Snapshot** tab on the right of the page.

4.  On the Interface Snapshot tab, click a TraceId link. The Link Invocation tab opens in a new window.

5.  Click the magnifier icon in the **Thread Profiling** column. The Thread Profiling dialog box appears.

**Note:**

-   The actual response time is the actual execution time for the service call, which is not affected by thread profiling.

-   The listening response time is the time consumed for TProf listening In general, the listening response time is approximately the actual response time minus the trigger threshold for slow calls.


**View thread profiling details through multi-dimensional query**

1.  In the left-side navigation pane of the console, choose **Application Monitoring** \> **Multi-dimensional Query**.

2.  On the Traces and Eventstab, select **Contain only thread profiling snapshots** from the **Parameter Name** drop-down list and then click **Query**.

![](http://icms-static-translation.oss-cn-hangzhou.aliyuncs.com/SP_177/DNARMS19100476/images/42296_zh-CN.png?Expires=1569140446&OSSAccessKeyId=LTAIJfoPL6wmrirR&Signature=urznqVji7osmylY0fg9UmFF%2FBqw%3D)

3.  Click a TraceId link in the search results. The Link Invocation tab opens in a new window.

4.  Click the magnifier icon in the **Thread Profiling** column.


## FAQ

Why are some slow calls not listened to?

A: If a large number of slow calls occur in a short period of time, to ensure the stability of the business system, ARMS limits listening resources for some slow calls.

