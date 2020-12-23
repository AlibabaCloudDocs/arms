# Use SkyWalking and tracing analysis to analyze slow requests at the code level

With the Java bytecode injection technology, many Java-based frameworks can implement automatic tracking to help you understand the specific tracking between which two slow requests occur. However, this is not enough to locate the problem at the code layer. If you need to locate the code that causes slow requests, you can use SkyWalking's slow request analysis feature and link tracking.

You have enabled link tracking through SkyWalking. For more information, see [Reporting Java application data by SkyWalking](/intl.en-US/Preparations/Start monitoring Java applications/Reporting Java application data by SkyWalking.md).

**Note:** Only SkyWalking 7.0 and higher versions have the slow request analysis feature.

## Create a slow request collection task

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **applications**. In the upper-left corner, select the target region and click the name of the target application on the **applications** page.

3.  In the left-side navigation pane, click **slow request analysis**, and then click **create task**.

4.  In the **create task** dialog box, set the following parameters, and click **OK**.

    |Parameter|Description|Required|Example|
    |---------|-----------|--------|-------|
    |Span name|The Span to be monitored.|Yes|/api|
    |Monitoring Time|The time when the monitoring starts. Select **current**, or select **set time** and set a custom time.|No|Now|
    |Monitoring duration|The duration of the monitoring.|No|5 min|
    |Span duration threshold|Only analyze the spans whose elapsed time exceeds this threshold. Unit: ms.|No|30 ms|
    |Monitoring interval|The interval at which the monitoring data is collected.|No|20 ms|
    |Maximum samples|The maximum number of spans for which data is collected. Valid values: 1 to 9.|No|5|

    The created task is displayed in the **task list**.


## Locate the methods that cause slow requests

After the specified monitoring duration starts with the monitoring time you set, the Span that exceeds the threshold is displayed in the **SampledTraces** area. Perform the following steps to locate the method that causes slow requests in the thread stack details on the right side of the page.

1.  On the **slow request analysis** page, click the target task in the **tasks** section.

    The spans with time consumption exceeding the threshold are displayed in the **SampledTraces** area.

2.  In the **SampledTraces** area, click the target Span, and observe the **thread stacks** area on the right side of the page.

    A method name that exceeds the specified threshold is displayed in red. You can optimize these methods accordingly.


## Why is no thread stack sampled after the monitoring duration ends?

If no thread stack is sampled after the monitoring duration ends, perform the following steps to troubleshoot the problem.

1.  On the **slow request analysis** page, find the target task in the **tasks** list and click **view task details** in the actions column.

2.  View the detailed information in the **task details** section of the **logs** dialog box.

    -   If the IP address of the Agent is displayed at the end of the **instance** field and the **action type** is `EXECUTION_FINISHED` or `EXECUTION_NOTIFY`, the network connection is normal because no such Span has exceeded the threshold.
    -   If it does not meet the above description, there is a problem with the network connection. Please try again later.

