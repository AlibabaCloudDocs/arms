# Analyze traces

On the Trace Analysis page of an application in the Tracing Analysis console, you can filter the traces of the application and view relevant charts and tables, including the application topology, the table of aggregated traces, and the waterfall chart of a trace.

## View trace information

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application that you want to check.

3.  In the left-side navigation pane, click **Trace Analysis**. On the Trace Analysis page, you can perform the following operations to filter traces:

    -   In the upper-left corner of the page, click the **Conditions** field. Then, specify filter conditions by setting one or more of the following parameters: **Span name**, **IP**, and **Label**. Each time when you specify filter conditions, you can add only one span name and IP address. However, you can add multiple tags at a time.
    -   Specify a response time in the **Takes Longer Than** field to query the information about the traces whose response time is longer than the specified response time.
    -   Select **Exceptions** to query the information about the exceptional traces.
4.  Click **Search** to view the information about the filtered traces. The trace information includes the following items:

    -   Time series curves of the elapsed time and span count
    -   Frequency distribution chart of spans by elapsed time
    -   Trace list in which traces can be grouped by span name or IP address
    ![Trace Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63933.png)

5.  To group traces, select Span or IP from the **Group By** drop-down list. The following figure shows that the traces are grouped by IP address.

    ![Trace List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63959.png)

6.  Click an IP address to view the traces that are related to this IP address.

    ![Trace List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63960.png)


## View the application topology

On the Application Topology tab, you can view an application topology which displays the dependencies between the current application whose traces are filtered and other applications. You can also view the request percentage, call multiplier, and elapsed time ratio between applications. For the best performance, the application topology feature aggregates the request data of up to 5,000 traces for the current application.

1.  Click the Application Topology tab to view the application topology.

    ![Trace Topology ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p66600.png)

    **Note:**

    -   The request percentage is calculated by dividing the number of requests involved when Application A calls Application B by the total number of requests received by Application A. Assume that 100 requests are received by Application A and only 90 requests are involved when Application A calls Application B. In this case, the request percentage of A to B is 90%. Some requests are sent to Application B because Application A may filter all the requests based on an IF statement.
    -   The call multiplier is calculated by dividing the number of spans involved when Application A calls Application B by the total number of spans received by Application A. Assume that 100 spans are received by Application A and 300 spans are involved when Application A calls Application B. In this case, the call multiplier of A to B is three. For example, the dependency from A to B is marked as 90%/3x, which indicates that 90% of the requests in Application A are sent to call Application B, and Application A calls Application B three times on average.

## View the table of aggregated traces

On the End-to-End Aggregation tab, you can view the filtered traces that are aggregated by span name and application name. For the best performance, the end-to-end aggregation feature aggregates the request data of up to 5,000 traces for the current application.

1.  Click the End-to-End Aggregation tab to view the table of aggregated traces.

    ![Trace Real-time Aggregation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p66616.png)

    **Note:**

    -   Request Count / Request Percentage: The request percentage is the ratio of the request count of the current span to the total request count. Assume that the total request count is 100 and the request percentage is 10%. In this case, 10 requests are sent to call the current span. The request percentage is calculated by dividing the request count of the current span by the total request count.
    -   Span Amount / Request Multiplier: The request multiplier indicates how many times each request calls the current span on average. For example, 1.5x indicates that each request calls the current span 1.5 times on average. The request multiplier is calculated by dividing the span count by the request count of spans.
    -   Average Self Elapsed Time / Percentage: The average self elapsed time of a span excludes the average elapsed time of its child spans. Assume that Span B is a child span of Span A. If the elapsed time of Span A is 10 ms and that of Span B is 8 ms, the self elapsed time of Span A is 2 ms. The self elapsed time of a span is calculated by deducting the sum of elapsed time of its child spans from the elapsed time of the span. For asynchronous calls, the elapsed time of child spans are not deducted.
    -   Exception Count / Exception Percentage: The exception percentage is the ratio of the count of exceptional requests to the total request count. For example, 3% indicates that 3% of all requests are exceptional. The exception percentage is calculated by dividing the count of exceptional requests by the total request count. The count of exceptional requests does not equal to the exception count. When the request multiplier is greater than 1, an exceptional request may have multiple exceptions.
2.  To view traces that are related to a span, move the pointer over the span name in blue. Click the ID of a trace. The waterfall chart of the trace appears. For more information, see [View the waterfall chart of a trace](#section_nn0_y6s_g63).


## View the waterfall chart of a trace

1.  Click the ID of a trace in the trace list. The waterfall chart of the trace appears.

    On the Traces page, you can view the trace information, including the span name, application name, status, IP address or server name, log generation time, and timeline.

    **Note:** The **IP Address** column may display IP addresses or server names. This depends on the display settings that are configured on the Application Settings page. For more information, see [Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md).

    ![Page Trace](../images/p63969.png "Traces page")

2.  Move the pointer over a span name to view the information about the span, including the duration, start time, tags, and log events.

    ![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p63977.png)


## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is `YYYY-MM-DD`, The time format is `HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

[Overview](/intl.en-US/Before you begin/Overview.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

