# Active profiling

The active profiling feature of Application Real-Time Monitoring Service \(ARMS\) application monitoring allows you to manually create and start active profiling tasks that listen to calls based on your business requirements.

Your application is monitored by ARMS. For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).

**Note:** To use the active profiling feature, you must upgrade the ARMS agent to V2.7.1.1 or later. For more information about how to upgrade the agent, see [Update the ARMS agent for Java applications](/intl.en-US/Application Monitoring/Update the ARMS agent for Java applications.md).

## Create an active profiling task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the **left-side navigation pane**, click **Active analysis**.

6.  In the New tasks section, set the parameters as required and click **Finish**.

    ![Active analysis - New tasks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6689340261/p242798.png)

    |Parameter|Description|
    |---------|-----------|
    |Interface name|The name of the API that you want the task to listen to.|
    |Thread profiling duration|The validity period of the task. Valid values:    -   5min
    -   10min
    -   15min |
    |Thread profiling trigger threshold \(ms\)|The duration that has elapsed before the task starts listening. For example, a slow call consumes 1.4s in total and this parameter is set to 100. In this case, the call is listened to only from the point in time when 100 ms has elapsed to the end of the call. Valid values: 50 to 30000. Unit: milliseconds.|
    |Thread profiling frequency \(ms\)|The intervals at which API snapshots are generated during thread profiling. The smaller the value, the higher the profiling accuracy, and the higher the performance overhead. We recommend that you set this parameter to 100. Valid values: 5 to 1000. Unit: milliseconds.|
    |Maximum number of samples|The maximum number of slow calls that the task can listen to. Valid values: 1 to 100|


## View the details of thread profiling

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the **left-side navigation pane**, click **Active analysis**.

6.  In the New tasks section, click **View historical tasks**.

7.  In the upper-right corner of the page, specify a time range. In the Task list section, click the name of the active profiling task that you want to view.

    After you specify a time range, the Task list displays all the active profiling tasks created within the time range.

    ![Active analysis - historical tasks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6689340261/p243147.png)

    In the right-side Thread analysis information section, you can view the information about the API calls listened to by the task, including trace IDs, the points in time when logs were generated, the names of the involved APIs, response codes, IP addresses, and time consumed.

    -   You can click a trace ID to view the details of the trace. For more information, see [Trace query](/intl.en-US/Application Monitoring/Console functions/Trace query.md).
    -   You can click **Thread analysis** in the **Details** column of a trace to view the thread profiling information about the trace.

        ![Thread Profiling](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6689340261/p243145.png)


## View the details of an active profiling task

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the **left-side navigation pane**, click **Active analysis**.

6.  In the New tasks section, click **View historical tasks**.

7.  In the Task list section, find the active profiling task that you want to view and click **Details** in the lower-right corner.

    On the Tasks tab, you can view the details of the task.

    ![Active analysis - task details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6689340261/p243943.png)

8.  Click the **Logs** tab.

    On the Logs tab, you can view the logs generated for the task.

    ![Active analysis - Logs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6689340261/p243944.png)


**Related topics**  


[Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application Monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)

