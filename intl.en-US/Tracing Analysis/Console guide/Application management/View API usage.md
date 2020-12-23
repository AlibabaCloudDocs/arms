# View API usage

The API invocation page displays the performance indicators of API calls in client calls, server calls, and local calls, as well as API calls of upstream and downstream links.

## View API call performance metrics

The **interface invocation** page lists all the interfaces \(spans\) involved in the application call. You can sort the list by response time, number of requests, or number of exceptions. Select an interface from the interface list. On the overview tab, you can view the topology of an application and the time sequence curves of the API call performance metrics, including the number of requests, response time, and variation constants.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **application list**. On the top of the application list page, select a region, and then click the application name.

3.  In the left-side navigation pane, click **interface invocation**. Click an interface in the left-side navigation pane, and then click the **overview** tab to view the topology and performance metrics of the interface.

    -   Click the **response time**, **requests**, **exceptions** tab, and then click the upward or downward arrow next to the tab. Then, you can sort all APIs in ascending or descending order by the specified condition.
    -   In the **call type** section, click **all**, **client**, **server**, or **local call** to filter the types of interfaces that need to be called.
    -   You can enter a keyword in the search box to dynamically filter API operations that meet the keyword.

**Note:** To switch to another application in the same region, click the application name drop-down list in the upper-left corner and select another application.

## View upstream and downstream services

The **upstream** interface and **downstream** interface tabs display the interfaces of the upstream application that calls the selected application and downstream application that calls the specified application and their performance metrics, including the number of requests, response time, and latency.

On the **upstream** and **downstream** tabs, you can perform the following operations as needed:

-   At the top of the tab, click **show /hide** all.
-   On the tabs, enter an application name or an interface \(span\) name in the search box, and click the magnifier icon to filter out the interfaces that meet corresponding conditions.
-   Click the collapse panel where the interface call information is located, or click the up or down arrow at the end of the row to expand or collapse the performance metric information of this interface call.

## View traces

The **Call link**

**Note:** **Status** The green icon in the column indicates that the time consumed is less than 500 milliseconds, the yellow icon indicates that the time consumed is between 500 milliseconds and 1000 milliseconds, the red icon indicates that the time consumed is greater than 1000 milliseconds, or the Tag Key is`Error`.

On the **Call link** tab page, you can perform the following operations as needed:

-   In **Time-consuming** enter a time value \(in milliseconds\) in the adjustment box, and click **Query** to filter traces whose time consumption is greater than the specified value.
-   Select **Exception** and click **Query** to filter out abnormal call links.
-   Click **Time consumed** Or **Status** By using the up and down arrows on the right, you can sort the query results in ascending or descending order.
-   Click the TraceID to open it in a new window. Call link Page, and view the waterfall chart of the call link.

## View trace waterfall chart

Onthe Call link page, you can check the log generation time, status, IP address/machine name, service name, and Timeline of the call link are displayed on the page.

**Note:** **IP address**Whether the IP address or machine name is displayed depends on Application Settings the display configuration on the page. For more information, see manage applications and tags.

![Page Traces](../images/p53827.png "Trace page")

Place the cursor over a service name to view the service duration, start time, Tag, and log event information.

![Overlay Tag and Log Events](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3806359851/p53828.png)

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is`YYYY-MM-DD`, The time format is`HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

**Related topics**  


[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

