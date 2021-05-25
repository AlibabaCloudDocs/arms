# Trace query

On the Call link query page, you can query the details of a specific trace based on the trace ID or query traces by using multiple filter conditions. You can also aggregate multiple traces for analysis.

## Query traces

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Invocation Trace Query**. In the top navigation bar, select a region.
3.  On the Call link query page, select a parameter from the **Parameter type** drop-down list, enter or select a value in the **Parameter value** field, and then click **Add to query criteria**.

    You can set the Parameter type parameter to TraceId for exact match.

    |Parameter|Description|
    |---------|-----------|
    |TraceId|Enter a trace ID.|
    |Interface name|Enter an API name. Fuzzy match is not supported.|
    |Client application name|Enter the name of an application on the client.|
    |Server application name|Enter the name of an application on the server.|
    |Time-consuming greater|Specify a number of milliseconds to query calls that take longer than the specified number of milliseconds.|
    |Call type|Select a call type.|
    |Abnormal call|Set this parameter to true to search for all traces that contain abnormal calls.|
    |Only thread profiling snapshots are included|Set this parameter to true to search for all traces that contain thread profiling snapshots.|
    |Client IP|Enter the IP address of an application that initiates the call.|
    |Server IP|Enter the IP address of an application that is called.|
    |Business primary key|Enter a business primary key to search for business events.|
    |Response code|Enter a response code.|

4.  Click the ID of the trace that you want to view to go to the Traces tab.

    ![Traces](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p43192.png)

    The following section describes the parameters on the Traces tab:

    -   Application Name: the name of the application to which the trace belongs.
    -   Log Generation Time: the time when the log was generated.
    -   Status: the status of the trace. Red indicates that an exception exists in the on-premises trace called by the service. Green indicates that the trace is normal.
    -   IP Address: the IP address of the application.
    -   Call Type: the type of the call, which corresponds to the call type of the ad hoc query.
    -   Service Name: the name of the service API that is called.
    -   Timeline: the time consumed by each service to call the trace and the proportion of time consumed by each service in the time consumed to call the entire trace.

## Analyze traces

On the Call link query page, select all the traces that you want to analyze and click **Analyze the selected call link**.

In the Call Chain Analysis pane, you can view the span name, application name, call type, number of requests, proportion of requests, number of exceptions, proportion of exceptions, average self consumed time, and average consumed time of all the selected traces.

![Trace aggregation for analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p187132.png)

-   Move the pointer over a span name to view the ID of the trace that contains the span.
-   Click an application name to go to the Application Overview page of the application.
-   Click **Statistical analysis** in the **Actions** column corresponding to a span to view details of the span. The details include the proportions of different call types for each API, total consumed time, API name, number of requests, recommended samples, number of times that each call method is used. The name, type, total time consumed, and proportion of time consumed by each call method are also included.

    ![Details of a span](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p187916.png)


## Supported operations

On the Traces tab, click the line chart in the **Indicator monitoring** column to view the number of requests, response time, and number of errors during different periods of time.

On the Traces tab, click the ![Magnifier](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8972658061/p185206.png) icon in the **Method Stack** column. The Method Stack pane appears.

![Method Stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p42284.png)

The following section describes the parameters in the Method Stack pane:

-   Method: the method used to call the on-premises method stack. After the call method is expanded, the next-layer calls of the method are displayed.
-   Line: the line where the code of the method used to call the on-premises method stack is located.
-   Expanded Info:
    -   Parameter: the input parameters of the call.
    -   SQL: the SQL statements to access data in the database.
    -   Exception: the details of the exception.
-   Timeline \(ms\): the distribution of time consumed by each method call of the on-premises trace.

