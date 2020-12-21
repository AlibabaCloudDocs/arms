# Trace query

On the Invocation Trace Query page, you can query the details about a specific trace by trace ID, or query traces by multiple filtering criteria.

TraceId: the unique ID of each trace, through which you can accurately query the calling data.

Trace: supports distributed traces, and supports querying inter-service traces and local service traces by using the local call method stack.

-   Distributed trace \(inter-service trace\): a trace between services.
-   Local trace \(method stack\): the local method stack of one-time inter-service traces.

Query traces by using either of the following methods:

-   Precise query: Select **TraceId** from the **Parameter Name** drop-down list. Enter the specific trace ID in the **Parameter Value** field, and click **Query**.
-   Advanced query: Query traces by setting multiple criteria.

## Portal

Follow these steps to access the Invocation Trace Query page.

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Invocation Trace Query**.

## Query traces

You can query a trace by specifying the trace ID or using multiple filtering criteria.

|Query field|Description|
|-----------|-----------|
|Call Type|-   HTTP Entry Point: The client uses HTTP protocol for calling.
-   Dubbo Call: The client uses Dubbo for calling.
-   HSF Call: The client uses HSF for calling. |
|Takes Longer Than|The consumed time for the call is longer than the specified milliseconds.|
|Show Abnormal Calls Only|Check this option to single out calls that throw exceptions.|
|Client Name/Client IP|The name and IP of the application that initiates the call.|
|Server Name/Server IP|The name and IP address of the called application.|
|Interface Name|The name of the interface called by the application. Prefix fuzzy match is supported. For example, you can use keyword api or resource to search for the /api/ResourceQuery interface.|

## View inter-service traces \(distributed traces\)

Go to the Distributed Invocation Trace page by clicking the trace ID of the trace you want to view.

![调用链聚合分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p187132.png)

## Field description

-   Status: whether the call is normal. Red indicates that an exception exists in the local trace of the service. Green indicates that the call is normal.

-   IP Address: the IP address of this application.

-   Call Type: the type of the call, which corresponds to the Call Type option of the ad hoc query.

-   Timeline: the time consumption of each inter-service trace, and time distribution of this trace relative to that of the entire trace.


## View local trace of the service \(method stack\)

On the Invocation Trace page, click the magnifier icon in the **Method Stack** column to go to the Method Stack page.

![方法栈](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p42284.png)

## Field description

-   Called Method: the method for calling the local method stack. After the call method is expanded, the next-layer calls of the method are displayed.

-   Line Number: the number of the line where the local method code is located.

-   Expansion information:

    -   Parameters: the input parameters of the call.
    -   SQL: the SQL statements called by the database.
    -   Exception: the details of exceptions and other information.
-   Timeline: the time distribution of every method call of the local trace.


