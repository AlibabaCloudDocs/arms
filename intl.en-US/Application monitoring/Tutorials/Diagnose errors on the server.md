# Diagnose errors on the server

It is challenging to analyze the causes of web page errors, which are one of the most common problems of Internet applications. After the Application Real-Time Monitoring Service \(ARMS\) agent is installed on an application, the ARMS agent can automatically capture, collect, count, and track exceptions without the need to modify the application code. You can use the ARMS agent to accurately locate all exceptions in the application and perform online diagnostics.

## Problem description

Web page errors, particularly those that take the form of a 5xx error, are one of the most common problems of Internet applications. 5xx errors usually occur on the server side. The server side has the most complex business logic and is the most error-prone part of the entire network-request link. Errors on the server side prove to be the most challenging for cause analysis. O&M engineers or development engineers often need to log on to the server to view logs and find the causes.

![Common error logs of Java applications](../images/p42274.png "Example: Common error logs of Java applications")

For applications that have less complex logic and short uptimes, the operation to log on to the server to view logs can solve most of these problems. However, this traditional method is often useless in the following scenarios:

-   You want to know the time and frequency of a specific type of error in a distributed application cluster.
-   A system has been running for a long time, but you do not care about the residual exceptions. You want to know only about new exceptions today compared with yesterday, and new exceptions after the release of the system compared with the period before the release of the system.
-   You view the web requests and relevant parameters associated with an exception.
-   Customer Services provides the number of an order that a user fails to place for cause analysis of the failure.

## Solution

Install the ARMS agent on the application. The ARMS agent can automatically capture, collect, count, and track exceptions without the need to modify the application code. The ARMS agent presents a clear picture of various errors.

## Step 1: Install the ARMS agent

The application can be monitored in all aspects only after you install the ARMS agent. Select one of the following methods to install the ARMS agent.

-   For more information about how to install the ARMS agent for a Java application, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md).
-   For more information about how to install the ARMS agent for a PHP application, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Quick start/Monitor PHP applications/Install the ARMS agent for a PHP application.md).
-   For more information about how to install the ARMS agent for an application in Enterprise Distributed Application Service \(EDAS\), see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Enable ARMS to monitor an EDAS application.md).
-   For more information about how to install the ARMS agent for an application in a Container Service Kubernetes cluster, see [t152230.md\#](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
-   For more information about how to install the ARMS agent for an application in an open source Kubernetes cluster, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

## Step 2: View statistics of application exceptions

The installed ARMS agent collects and shows the average response time and number of requests, errors, real-time instances, full garbage collection \(GC\) events, slow SQL queries, exceptions, and slow calls of the application within the selected period of time. The ARMS agent also shows how these metrics change on a day-over-day and week-over-week basis. Perform the following steps to view the statistics of application exceptions:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  In the top navigation bar, select the region where your application is deployed.

4.  On the **Applications** page, click the name of your application.

5.  On the **Application Overview** page, click the **Overview** tab. On the Overview tab, the total number of exceptions and how the number changes from the previous day and previous week are displayed in the lower part.

    ![Count of exceptions](../images/p47240.png "Count of exceptions")

6.  Scroll to **Exception Type** in the **Statistics Analysis** section at the bottom of the **Overview** tab. Here you can view the number of times for which each type of exception occurs.

    ![The number of times each type of exception occurs](../images/p42279.png "The number of times each type of exception occurs")

7.  In the left-side navigation pane, click **Application Details**. On the Application Details page, click the **Exception Analysis** tab in the right-side pane to view the exception statistics chart, count of errors, and exception stack.

    ![Exception Analysis tab](../images/p42280.png "Exception Analysis tab")


## Step 3: Diagnose causes of exceptions

The statistics of application exceptions are insufficient for locating the causes of exceptions. The exception stack in the log contains the code snippet for a call. However, it does not contain the complete upstream and downstream information and request parameters of this call. The bytecode enhancement technology of the ARMS agent allows you to capture complete upstream and downstream call snapshots for exceptions, and the compromise to performance is small. Then, you can identify the specific causes of exceptions.

1.  On the **Exception Analysis** tab, find the type of exception that you want to diagnose, and click **Interface Snapshot** in the **Actions** column.

    On the **Interface Snapshot** tab, the call trace information related to this exception type is displayed.

2.  On the **Interface Snapshot** tab, click the TraceId of a problem call.

    **Note:** For more information about how to find the trace of a problem call, see [Trace query](/intl.en-US/Application monitoring/Console functions/Trace query.md).

    ![Interface Snapshot tab](../images/p42281.png "Interface Snapshot tab")

3.  On the page that appears, view the trace information about the problem call. In the **Method Stack** column, click the magnifier icon to view the method stack that is called. This way, you can obtain the context information about this problem call.

    ![Complete trace information of the problem call](../images/p42282.png "Complete trace information of the problem call")

    At this point, the causes of the exception are found. This effectively helps you with the subsequent code optimization. You can also return to the Interface Invocation tab to view other problem calls in the list and solve related exceptions one by one.


## What to do next

To prevent passive diagnostics after an exception occurs, you can also use the alert feature of ARMS to create an alert for a specific API or all APIs. This ensures that the O&M team receives a notification immediately after an exception occurs. For more information about how to create an alert, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

## References

-   [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)
-   [t152244.md\#](/intl.en-US/Application monitoring/Console functions/API monitoring.md)
-   [Trace query](/intl.en-US/Application monitoring/Console functions/Trace query.md)
-   [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)
-   [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

