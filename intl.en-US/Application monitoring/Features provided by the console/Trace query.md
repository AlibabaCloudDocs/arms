# Trace query

On the Call link query page, you can query the details about a specific trace based on the trace ID or query traces by using multiple filter conditions. You can also perform aggregation analysis on multiple traces.

## Query traces

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Invocation Trace Query**. In the top navigation bar, select a region.
3.  On the Call link query page, select a parameter from the **Parameter type** drop-down list, enter a custom tag in the **Parameter value** field, and then click **Add to query criteria**.

    You can set Parameter type to TraceId for exact match.

    |Parameter|Description|
    |---------|-----------|
    |TraceId|Enter a trace ID.|
    |Interface name|Enter an operation name. Fuzzy match is not supported.|
    |Client application name|Enter the name of an application on the client.|
    |Server application name|Enter the name of an application on the server.|
    |Time-consuming greater|Specify a number of milliseconds to query calls that take longer than the specified number of milliseconds.|
    |Call type|Select a call type.|
    |Abnormal call|Set this parameter to true to search for all traces that contain abnormal calls.|
    |Only thread profiling snapshots are included.|Set this parameter to true to search for all traces that contain thread profiling snapshots.|
    |Client IP|Enter the IP address of an application that initiates the call.|
    |Server IP|Enter the IP address of an application that is called.|
    |Business primary key|Enter a business primary key to search for business events.|
    |Response code|Enter a response code.|

4.  Click the ID of the trace that you want to view to go to the Trace Details page.

    ![Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p43192.png)

    The following section describes the parameters on the Trace Details page:

    -   Application Name: the name of the application to which the trace belongs.
    -   Log generation time: the time when the log was generated.
    -   Status: Red indicates that an exception exists in the local trace called by the service. Green indicates that the trace is normal.
    -   IP Address: the IP address of the application.
    -   Call Type: the type of the call, which corresponds to the call type of the ad hoc query.
    -   Service Name: the name of the service operation that is called.
    -   Timeline: the time consumed by each service to call the trace and the proportion of time consumed by each service in the time consumed to call the entire trace.

## Analyze traces

On the Call link query page, select all the traces that you want to analyze and click **Analyze the selected call link**.

In the Call Chain Analysis panel, you can view the span name, application name, call type, number of requests, proportion of requests, number of exceptions, proportion of exceptions, average self-consumed time, and average consumed time of all the selected traces.

![Aggregation analysis of traces](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p187132.png)

-   Move the pointer over a span name to view the trace ID that contains the span.
-   Click an application name to go to the Application Overview page of the application.
-   Click **Statistical analysis** in the **Actions** column corresponding to a span to view details about the span. The details include the proportions of different call types for each operation, total consumed time, operation name, number of requests, recommended samples, the number of times that each calling method is used, as well as the name, type, execution time, and time percentage of each calling method.

    ![Details about a span](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p187916.png)


## Related operations

On the Trace Details page, click the line chart in the **Metric Monitored** column to view the number of requests, response time, and number of errors during different periods of time.

On the Trace Details page, click the ![Magnifier](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8972658061/p185206.png) icon in the **Method Stack** column. The Method Stack dialog box appears.

![Method Stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p42284.png)

The following section describes the parameters in the Method Stack dialog box:

-   Calling Method: the method used to call the local method stack. When the Calling Method section is shown, the next calls of the method are displayed.
-   Line Number: the number of the line where the code of the local method is located.
-   Extended Information:
    -   Parameter: input parameters of the call
    -   SQL: SQL statements to call the database
    -   Exception: exception details
-   Timeline: the distribution of time consumed by each method call of the local trace.

