# Use SkyWalking and Tracing Analysis to analyze slow requests at the code level

Based on the Java bytecode injection technology, many Java frameworks can be used to automatically instrument applications. This way, you can know the spans between which a slow request occurs. However, this is not enough to identify issues at the code level. You can use the slow request analysis feature of SkyWalking and Tracing Analysis to find the specific methods that cause slow requests.

SkyWalking is connected to Tracing Analysis. For more information, see [Use SkyWalking to report Java application data](/intl.en-US/Before you begin/Monitor Java applications/Use SkyWalking to report Java application data.md).

**Note:** Only SkyWalking 7.0 or later has the slow request analysis feature.

## Create a slow request collection task

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. In the upper-left corner of the **Applications** page, select a region as required. Then, click the name of the application that you want to check.

3.  In the left-side navigation pane, click **Slow Request Analysis**. Then, click **Create a task**.

4.  In the **Create a task** dialog box, set the parameters as required and click **OK**.

    ![Create a slow request analysis task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0222239061/p139671.png)

    |Parameter|Description|Required|Example|
    |---------|-----------|--------|-------|
    |Span name|The span to be monitored.|Yes|/api|
    |Monitoring time|The time when the monitoring starts. Select **Now**, or select **Set time** and specify a custom time.|No|Now|
    |Monitoring duration|The duration of the monitoring.|No|5 min|
    |Span time-consuming threshold|The threshold of the span duration. The span is analyzed only when its duration exceeds this threshold. Unit: ms.|No|30 ms|
    |Monitoring interval|The interval at which monitoring data is collected.|No|20 ms|
    |Maximum number of samples|The maximum number of data samples that are collected for the span. Valid values: 1 to 9.|No|5|

    The created task is displayed in the **Task list** section.


## Find the methods that cause slow requests

After the specified monitoring duration that starts from the specified monitoring time, the spans whose duration exceeds the threshold are displayed in the **Sampled Traces** section. Perform the following steps to find the methods that cause slow requests based on the detailed information of thread stacks on the right of the page:

1.  On the **Slow Request Analysis** page, click the task that you created in the **Task list** section.

    The spans whose duration exceeds the threshold are displayed in the **Sampled Traces** section.

2.  In the **Sampled Traces** section, click the span that you want to check. Then, view the content in the **Thread Stack** section on the right of the page.

    Methods whose duration exceeds the specified threshold are displayed in red. You can optimize these methods.


## Why is no thread stack sampled after the monitoring duration ends?

If no thread stack is sampled after the monitoring duration ends, perform the following steps to troubleshoot the issue:

1.  In the **Task list** section of the **Slow Request Analysis** page, click **View task details** to the right of the task that you created.

2.  View the detailed information in the **Log** section of the **Task details** dialog box.

    -   If the value of the **Instance** parameter contains the monitored agent IP address at the end and the value of the **Operation Type** parameter is `EXECUTION_FINISHED` or `EXECUTION_NOTIFY`, the network connection is normal. No thread stack is sampled because no span whose duration exceeds the threshold exists.
    -   If the preceding conditions are not met, the network connection is abnormal. Try again later.

