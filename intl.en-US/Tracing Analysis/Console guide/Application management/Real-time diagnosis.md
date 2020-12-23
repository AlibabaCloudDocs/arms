# Real-time diagnosis

After the data is reported to the Tracing Analysis component, the Tracing Analysis component performs real-time aggregate computing on the data. Generally, there is a certain delay. If you want to see the real-time result when locating a problem, you can use the real-time diagnosis function to quickly display the diagnostic result.

-   Real-time diagnostics enables temporary storage. After data is reported, you can quickly display diagnostic results without real-time statistics.
-   Real-time diagnosis does not affect normal statistics, and is automatically disabled in five minutes. After the function is disabled, you can enable it again.
-   By default, the real-time diagnosis page is refreshed regularly every 10 seconds. You can also disable the timed refresh function.

## View trace information

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click**Application List**, And inApplication ListSelect a region and click the name of the target application.

3.  In the left-side navigation pane, click**Real-time diagnosis**, InReal-time diagnosisPage. Click the + icon on the top to add**Span name**,**IP**And**Tag**Three filter criteria.

    **Note:** When you add a filter, you can add one**Span name**Or**IP**And multiple**Tag**.

4.  Click**Query**To view the filtered trace information, including:

    -   The scatter chart of real-time request response time distribution.

        **Note:** You can select an area in a scatter chart to obtain the real-time diagnostic results for this area.

    -   Request count/time consumption distribution chart.
    -   The list of trace information.

## View the waterfall chart of call traces

1.  Click a trace ID in the trace list. The waterfall chart appears.

    On the trace page, you can view the trace information such as the Span name, application name, status, IP address /machine name, log generation time, and timeline.

    **Note:** The **IP** address field displays the IP address or machine name, depending on the display configuration on the app settings page. For more information, see [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md).

    ![Page Trace](../images/p63969.png "Link page")

2.  Move the pointer over a Span to view the time, start time, Tag, and event log of the Span.

    ![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4876458061/p63977.png)


## View the interface aggregation list

1.  ClickInterface aggregationTab to view the list of API aggregates that aggregate call chains by Span name.


