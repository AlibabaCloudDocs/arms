---
keyword: [ARMS, EDAS, API, call, SQL, upstream and downstream]
---

# API monitoring

The API monitoring feature is used to monitor the details of API calls of an application. This feature allows you to monitor the SQL analysis, NoSQL analysis, exception analysis, error analysis,upstream and downstream services, and API call snapshots.

## Go to the Interface Invocation page

To go to the Interface Invocation page, perform the following steps:

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.
3.  On the Applications page, click the application that you want to view.
4.  In the left-side navigation pane, click **Interface Invocation**.

## Frameworks

This feature can automatically detect and monitor the APIs provided in the following web frameworks and remote procedure call \(RPC\) frameworks:

-   Tomcat 7+
-   Jetty 8+
-   Resin 3.0+
-   Undertow 1.3+
-   WebLogic 11.0+
-   SpringBoot 1.3.0+
-   HSF 2.0+
-   Dubbo 2.5+

## View the details of an API

On the Overview tab, you can view the detailed call topology of an API and the time sequence curves of the request count, response time, error count, and HTTP status codes.

![ARMS Application Monitoring - Interface Invocation - Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64160.png)

## View SQL and NoSQL analysis

On the SQL Analysis and NoSql Analysis tabs, you can view the SQL and NoSQL requests that are initiated within the code of the selected API in the left-side pane. On these tabs, you can find the SQL statements or NoSQL statements that cause slow responses of an API. You can also click **Interface Snapshot** in the Actions column of an SQL or NoSQL statement to view the complete trace where the SQL or NoSQL execution logic resides.

![ARMS - Application Monitoring - Interface Invocation - SQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64163.png)

## View exception analysis

On the Exception Analysis tab, you can view the Java exceptions that are thrown from the code of the selected API in the left-side pane. You can also click **Interface Snapshot** in the Actions column of an exception to view the complete trace where the exception stack resides.

![ARMS Application Monitoring - Interface Invocation - Exception Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64166.png)

## View error analysis

On the Error Analysis tab, you can view the errors and HTTP status codes of the application. You can also click a value in the TraceId column to view the trace information on a new page.

![Error Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p75826.png)

## View upstream and downstream services

On the **Upstream Services** and **Downstream Services** tabs, you can view the APIs and performance metrics of the upstream services that call the application and downstream services that are called by the application. The performance metrics include the response time, number of requests, and number of errors.

![ARMS Application Monitoring - Interface Invocation - Upstream Services](../images/p64182.png "Upstream Services tab")

On the **Upstream Services** and **Downstream Services** tabs, you can perform the following operations based on your business requirements:

-   On the tabs, click **Collapse/Expand All** to collapse or expand all APIs.
-   On the tabs, enter a keyword of application names or API \(span\) names in the search box and click the Search icon to search for the APIs whose names contain the keyword.
-   Click the collapse panel where the API information resides, or click the up or down arrow at the end of the row. You can then expand or collapse the performance metric information of the API.

## View API snapshots

On the Interface Snapshot tab, you can view the parameters of the selected API and two charts that are generated based on the parameters. The charts display the statistics on the total number of snapshots and snapshot response time.

![ARMS Application Monitoring - Interface Invocation - Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6122117161/p75784.png)

-   The Total snapshots chart, which is marked as 1 in the preceding figure, displays the numbers of normal snapshots and slow snapshots over time. In this example, the snapshots for which the response time of API calls exceeds 500 milliseconds are defined as slow snapshots. The number of slow snapshots is affected by the value of the Interface Response Time Threshold parameter that you specify in the application configurations. Slow snapshots does not include the sub snapshots that are captured for the asynchronous calls of on-premises APIs.

    **Note:** In the Total snapshots chart, the number of normal snapshots refers to the total number of snapshots, which includes the number of slow snapshots.

-   The Snapshot response time chart, which is marked as 2 in the preceding figure, displays the trends in response time over time. The chart is generated based on the statistics of API snapshots and is affected by the sampling rate that you specify.
-   The parameter details table, which is marked as 3 in the preceding figure, displays the detailed information about the parameters of the selected API. You can click a value in the TraceId column to view the trace information and business information. You can also click **View Logs** in the Actions column to view the logs of API calls.

