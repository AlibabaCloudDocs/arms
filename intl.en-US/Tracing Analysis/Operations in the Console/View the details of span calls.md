# View the details of span calls

On the Interface Calls page, you can view the performance metrics of span calls on the client, span calls on the server, and internal span calls for an application. You can also view the details of span calls for upstream services that call the application and downstream services that are called by the application.

## View the performance metrics of span calls

On the **Interface Calls** page of an application, you can view all the spans that are involved in application calls. You can sort the spans by response time, number of requests, or number of errors. After you click a span in the span list, the Overview tab displays the topology of the span and the line charts for the performance metrics of span calls. The performance metrics include the number of requests, response time, and number of errors.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application that you want to check.

3.  In the left-side navigation pane, click **Interface Calls**. In the left-side span list, click the span that you want to view. Then, view the topology of the span and the performance metrics of span calls on the **Overview** tab.

    -   You can click the **Response Time**, **Requests**, or **Exceptions** tab and click the upward or downward arrow next to the tab name to sort spans in ascending or descending order based on the corresponding conditions.
    -   You can set the **Call Type** parameter to **All**, **Client**, **Server**, or **Local Calls** to list all spans of the specified call type.
    -   You can enter a keyword in the search box and click the search icon to filter spans.

**Note:** To switch to another application in the same region, click the application name drop-down list in the upper-left corner and select another application.

## View the details of span calls for upstream and downstream services

On the **Upstream Traces** and **Downstream Traces** tabs, you can view the spans of upstream services that call the application and downstream services that are called by the application, and the performance metrics of span calls. The performance metrics include the number of requests, response time, and number of errors.

![Downstream Spans](../images/p53842.png "Downstream Traces tab")

On the **Upstream Traces** and **Downstream Traces** tabs, you can perform the following operations based on your business requirements:

-   On the tabs, click **Expand/Collapse All** at the top to show or hide all spans.
-   On the tabs, enter a keyword in the search box at the top and click the search icon to filter spans based on the application name or span name.
-   Click the collapse panel where the information about a span resides, or click the upward or downward arrow at the end of the row. You can then show or hide the performance metric information of the span.

## View traces

The **Call link**

![Tab Traces](../images/p53826.png "Trace tab")

**Note:** **Status** The green icon in the column indicates that the time consumed is less than 500 milliseconds, the yellow icon indicates that the time consumed is between 500 milliseconds and 1000 milliseconds, the red icon indicates that the time consumed is greater than 1000 milliseconds, or the Tag Key is `Error`.

On the **Call link** tab page, you can perform the following operations as needed:

-   In **Time-consuming** enter a time value \(in milliseconds\) in the adjustment box, and click **Query** to filter traces whose time consumption is greater than the specified value.
-   Select **Exception** and click **Query** to filter out abnormal call links.
-   Click **Time consumed** Or **Status** By using the up and down arrows on the right, you can sort the query results in ascending or descending order.
-   Click the TraceID to open it in a new window. Call link Page, and view the waterfall chart of the call link.

## View trace waterfall chart

Onthe Call link page, you can check the log generation time, status, IP address/machine name, service name, and Timeline of the call link are displayed on the page.

**Note:** **IP address** Whether the IP address or machine name is displayed depends on Application Settings the display configuration on the page. For more information, see manage applications and tags.

![Page Traces](../images/p53827.png "Trace page")

Place the cursor over a service name to view the service duration, start time, Tag, and log event information.

![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3806359851/p53828.png)

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is `YYYY-MM-DD`, The time format is `HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

**Related topics**  


[Overview](/intl.en-US/Before you begin/Overview.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

