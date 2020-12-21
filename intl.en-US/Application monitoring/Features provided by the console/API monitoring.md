---
keyword: [ARMS, EDAS, APIs, calls, SQL, upstream and downstream]
---

# API monitoring

The API monitoring feature is used to monitor the details of API calls of an application. This feature allows you to monitor the SQL analysis, NoSQL analysis, exception analysis, error analysis,upstream and downstream services, and API call snapshots.

## Procedure

To go to the Interface Invocation page, perform the following steps:

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.
2.  On the Applications page, click the application that you want to view.
3.  In the left-side navigation pane, click **Interface Invocation**.

## Framework

This feature module can automatically detect and monitor the APIs provided in the following web frameworks and remote procedure call \(RPC\) frameworks:

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

On the SQL Analysis and NoSQL Analysis tabs, you can view the SQL and NoSQL requests that are initiated within the code of the selected APIs in the left-side navigation pane. On this tab, you can find the SQL statements or NoSQL statements that cause slow responses of a service. You can also click **Interface Snapshot** in the Actions column of an SQL or NoSQL statement to view the complete code trace where the SQL or NoSQL execution logic resides.

![ARMS - Application Monitoring - Interface Invocation - SQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64163.png)

## View exception analysis

On the Exception Analysis tab, you can view the Java exceptions that are thrown from the code of the selected APIs in the left-side navigation pane. You can also click **Interface Snapshot** in the Actions column of an exception to view the complete trace where the exception stack resides.

![ARMS Application Monitoring - Interface Invocation - Exception Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64166.png)

## View error analysis

On the Error Analysis tab, you can view the errors and HTTP status codes of the application. You can also click a value in the TraceId column to view the trace information on a new page.

![Error Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p75826.png)

## View upstream and downstream services

On the **Upstream Services** and **Downstream Services** tabs, you can view the APIs and performance metrics of the upstream services that call the application and downstream services that are called by the application. The performance metrics include the response time, request count, and error count.

![ARMS Application Monitoring - Interface Invocation - Upstream Services](../images/p64182.png "Upstream Services tab")

On the **Upstream Services** and **Downstream Services** tabs, you can perform the following operations based on your business requirements:

-   On the tabs, click **Collapse/Expand All** to collapse or expand all APIs.
-   On the tabs, enter an application name or an API \(span\) name in the search box, and click the Search icon to search the APIs that meet corresponding conditions.
-   Click the collapse panel where the API information resides, or click the up or down arrow at the end of the row. You can then expand or collapse the performance metric information of the API.

## View interface snapshots

On the Interface Snapshot tab, you can view the parameters of the selected APIs. You can click the trace ID to view the trace.

![ARMS Application Monitoring - Interface Invocation - Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4761458061/p75784.png)

