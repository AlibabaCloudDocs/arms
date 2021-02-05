# Diagnose application freezing

It is difficult to locate and troubleshoot the causes of application freezing. Application Monitoring of Application Real-Time Monitoring Service \(ARMS\) provides a set of solutions, such as thread profiling, trace diagnostics, and API monitoring. These solutions help you locate all slow calls in an application and solve application freezing problems.

## Cause

Website freezing and slow web page loading are among the most common problems of Internet applications. Troubleshooting and solving these problems is complex and takes a long time. This is due to the following reasons:

-   Overly long application traces
    -   The cause can be a failure at a stage of a long trace. The failure can happen from the frontend web page to the backend gateway, or from the web application server to the backend database.
    -   Applications that use microservice architectures have even more complex traces, and different components of applications may be maintained by different teams and personnel. This makes troubleshooting more difficult.
-   Incomplete or low-quality logs

    Most methods of troubleshooting online problems rely on application logs. However, the locations of problems are usually unpredictable, and slow response frequently occurs. To find the true causes of slow response, you need to print the log in every place where errors may occur and record each call. The cost is very high for doing so.

-   Insufficient monitoring

    Rapid business development and fast application iteration lead to frequent API changes of applications and increased dependencies. This further deteriorates the quality of code. Applications need a comprehensive monitoring system that automatically monitors every API of the application and records abnormal calls.


## Solution

After the ARMS agent is installed, you can monitor all slow calls of your application by using features such as thread profiling, trace diagnostics, and API monitoring of ARMS Application Monitoring. Also, you do not need to modify the application code.

## Step 1: Install the ARMS agent for a Java application

You can use ARMS Application Monitoring to monitor your application in all aspects only after you install the ARMS agent. Select one of the following methods to install the ARMS agent.

-   For more information about how to install the ARMS agent for a Java application, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md).
-   For more information about how to install the ARMS agent for a PHP application, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Quick start/Monitor PHP applications/Install the ARMS agent for a PHP application.md).
-   For more information about how to install the ARMS agent for an application in Enterprise Distributed Application Service \(EDAS\), see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Enable ARMS to monitor an EDAS application.md).
-   For more information about how to install the ARMS agent for an application in a Container Service Kubernetes cluster, see [t152230.md\#](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
-   For more information about how to install the ARMS agent for an application in an open source Kubernetes cluster, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

## Step 2: View statistics of slow SQL queries

The installed ARMS agent collects and shows the average response time and number of requests, errors, real-time instances, full garbage collection \(GC\) events, slow SQL queries, exceptions, and slow calls of the application within the selected period of time. The ARMS agent also shows how these metrics change on a day-over-day and week-over-week basis. Perform the following steps to view the statistics of slow SQL queries.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  In the top navigation bar, select the region where your application is deployed.

4.  On the **Applications** page, click the name of your application.

5.  On the **Application Overview** page, click the **Overview** tab. On the Overview tab, the total number of slow SQL queries and how the number changes from the previous day and previous week are displayed.


## Step 3: Find and locate slow APIs

On the **Interface Invocation** page, all APIs provided by the monitored application, and the number of calls and consumed time on each API are displayed. Slow APIs are marked to help you find and locate them.

1.  In the left-side navigation pane, click **Interface Invocation**.
2.  In the left-side navigation page of the **Interface Invocation** page, click the most frequently invoked slow API to view its details in the right-side pane.

    ![Interface invocation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8458342161/p47127.png)


## Step 4: View and locate the problem code

After you locate a slow API, you must find the problem code to eliminate the problem. A snapshot is a complete record of an entire trace. The snapshot includes the code and time consumption of each call, and helps you precisely locate the problem code.

1.  On the **Interface Invocation** page, click the **Interface Snapshot** tab.

    On the **Interface Snapshot** tab, all snapshots of the API are displayed.

2.  On the **Interface Snapshot** tab, click the TraceId of a call that may have code problems.

3.  On the page that appears, view the call trace information related to the exception. In the **Method Stack** column, click the magnifier icon to view the method stack that is called. This way, you can obtain the context information about the exception.

    **Note:** For more information about how to find the trace of a problem call, see [.](/intl.en-US/Application monitoring/Console functions/Trace query.md)

    At this point, the causes of a specific slow call are revealed. This effectively helps you with the subsequent code optimization. You can also return to the Interface Invocation page to view other slow calls in the list and solve them one by one.


## What to do next

To prevent passive diagnostics after an exception occurs, you can also use the alert feature of ARMS to create an alert for a specific API or all APIs. This ensures that the O&M team receives a notification immediately after an exception occurs. For more information about how to create an alert, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

## References

-   [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)
-   [t152244.md\#](/intl.en-US/Application monitoring/Console functions/API monitoring.md)
-   [Trace query](/intl.en-US/Application monitoring/Console functions/Trace query.md)
-   [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)
-   [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

