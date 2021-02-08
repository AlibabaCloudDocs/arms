# Perform real-time diagnostics

After data is reported to Tracing Analysis, the components of Tracing Analysis perform aggregate computing on the data in real time. Generally, the result is available with a specific latency. If you want to view the real-time diagnostics result during troubleshooting, you can use the real-time diagnostics feature.

-   When you use the real-time diagnostics feature, a temporary storage mechanism is enabled. After data is reported, the diagnostics result is displayed without the need of real-time statistics.
-   The real-time diagnostics feature does not affect normal statistics. This feature is automatically disabled after 5 minutes. After the feature is disabled, you can enable the feature again.
-   By default, the real-time diagnostics page is refreshed at intervals of 10 seconds. You can also disable the scheduled refresh feature.

## View the trace information

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application for which you want to view the trace information.

3.  In the left-side navigation pane, click **Real-time Diagnosis**. On the Real-time Diagnosis page, click the + icon at the top and add one or all of the **Span Name**, **IP**, and **Tag** filters.

    **Note:** You can add a **Span Name** filter, an **IP** filter, or multiple **Tag** filters.

4.  Click **Query** to view the following trace information that is obtained based on the specified filters:

    -   The bitmap of the response time distribution of real-time requests

        **Note:** You can box-select an area on the bitmap to obtain the real-time diagnostics result of this area.

    -   The chart that shows the number of requests and the elapsed time distribution of requests
    -   The list of traces

## View the waterfall chart of a trace

1.  Click the ID of a trace in the trace list. The waterfall chart of the trace appears.

    On the Traces page, you can view the trace information, including the span name, application name, status, IP address or server name, log generation time, and timeline.

    **Note:** The **IP Address** column may display IP addresses or server names. This depends on the display settings that are configured on the Application Settings page. For more information, see [Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md).

    ![Page Trace](../images/p63969.png "Traces page")

2.  Move the pointer over a span name to view the information about the span, including the duration, start time, tags, and log events.

    ![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p63977.png)


## View the list of aggregated traces

1.  Click the Interface Aggregation tab to view the list of traces that are aggregated based on the span name.


