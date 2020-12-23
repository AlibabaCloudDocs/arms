# Analyze a trace

After analyzing the trace of an application on the trace analysis page, you can filter the trace by condition and view the application topology, real-time aggregate table, and trace waterfall chart.

## View information of traces

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **application list**. On the top of the application list page, select a region, and then click the name of the target application.

3.  In the left-side navigation pane, click **call chain analysis**. On the call chain analysis page, you can filter the trace information, as shown in the following figure.

    -   You can click the **synthesis conditions** field in the upper-left corner to add **Span name**, **IP**, and **tag** at the same time or separately. When adding a filter, you can add a single **Span name** or **IP**, and multiple **tags**.
    -   Enter the specific response time in the **time elapsed** greater than box to query the trace information that takes more than this time.
    -   Select the **abnormal** check box to query the traces that have exceptions.
4.  Click **search** to view the filtered trace information, including:

    -   Time sequence curves of the elapsed time and Span count.
    -   Charts of spans /time consumption distribution.
    -   The list of traces for filtering groups by Span or IP.
    ![Trace Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63933.png)

5.  Select Span or IP address from the **group** by list to filter groups. For example, select the **IP**.

    ![Trace List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63959.png)

6.  Click an IP address to view the list of traces related to this IP address.

    ![Trace List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7955458061/p63960.png)


## View the application topology

The application topology section displays the topology of the dependencies among the applications filtered by conditions, and displays the request ratio, call multiple, and time consumption ratio of each application. For the sake of performance and experience, the application topology supports pulling up to 5,000 links of requests for aggregation.

1.  Click the application topology tab to view the application topology.

    ![Trace Topology ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p66600.png)

    **Note:**

    -   Request percentage=number of requests called by an application /total number of requests from the application. For example, if 100 requests are sent to application A and only 90 requests are sent to application B, the percentage of requests from application A to application B is 90%. \( \(In Application A, some requests may not be sent to application B because the if judgment is used for filtering.\)
    -   Call multiple=number of spans accessed by the application /total number of spans. For example, 100 spans enter application A and 300 spans call Application B from application A. The multiple of A to B is 3. For example, 90% of requests from application A to application B are scheduled to call Application B three times.

## View the real-time link aggregation table

Real-time aggregation is a call link table that aggregates the filtered traces by Span name and application name. For performance-based, real-time aggregation allows you to pull up to 5,000 links of requests.

1.  Click the full link aggregation tab to view the real-time link aggregation table.

    ![Trace Real-time Aggregation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p66616.png)

    **Note:**

    -   Requests /requests: the percentage of the requests that make the most of the requests. For example, if the total number of requests is 100 and the request percentage is 10%, it indicates that 10 requests call the current Span. Calculation formula=number of requests for the current Span /total number of requests X 100%.
    -   Span /request multiple: the multiple of requests indicates the average number of times that each request calls the current Span. For example, 1.5x indicates the average number of times each request calls the current Span 1.5. The number of requests calculated by the formula=number of spans /Number of spans.
    -   Average self-elapsed time /proportion: the average self-elapsed time does not include the average elapsed time of sub-spans. For example, if A requires 10 milliseconds for A to B, and B requires 8 milliseconds for A, then A requires 2 milliseconds for itself. Formula=Span elapsed time-Sum \(sub-Span elapsed time\). In an Asynchronous call, the sub-elapsed time is not deducted. The elapsed time is calculated as follows:=Span.
    -   Abnormal /abnormal rate: the percentage of abnormal requests. For example, 3% indicates 3% of abnormal requests. =number of abnormal requests /total number of requests The number of abnormal requests is not equal to the number of exceptions. When the request count is greater than 1, one exception request may have multiple exceptions.
2.  Move the pointer over a blue Span to view the prompts for a recommended trace. You can view the traces associated with this Span. Click a traceId to display a trace waterfall chart. For more information, see [View the waterfall chart of call traces](#section_nn0_y6s_g63).


## View the waterfall chart of call traces

1.  Click a trace ID in the trace list. The waterfall chart appears.

    On the trace page, you can view the trace information such as the Span name, application name, status, IP address /machine name, log generation time, and timeline.

    **Note:** The **IP** address field displays the IP address or machine name, depending on the display configuration on the app settings page. For more information, see [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md).

    ![Page Trace](../images/p63969.png "Link page")

2.  Move the pointer over a Span to view the time, start time, Tag, and event log of the Span.

    ![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p63977.png)


## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is`YYYY-MM-DD`, The time format is`HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

