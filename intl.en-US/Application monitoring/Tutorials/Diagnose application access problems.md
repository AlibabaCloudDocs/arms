# Diagnose application access problems

The locating and troubleshooting of the causes for application access problems present many challenges. Application Monitoring of Application Real-Time Monitoring Service \(ARMS\) provides a set of solutions, such as thread profiling, tracing diagnosis, and API monitoring. These solutions help you quickly and accurately locate all slow calls in an application and solve the application access problems.

## Analysis

Website freezing and slow webpage loading are among the most common problems of Internet applications. Troubleshooting and solving these problems is complex and takes a long time. Here are the major reasons:

-   Overly long application tracing
    -   The cause can be any failure at any stage of the long trace. The failure can happen between the front-end webpage and the back-end gateway, or between the web application server and the back-end database.
    -   Applications using the microservice architecture have even more complex traces. Different components of applications might be maintained by different teams and persons, which makes troubleshooting more difficult.
-   Incomplete or low-quality logs
    -   Most methods of troubleshooting online problems rely on application logs. However, the locations of problems are often unpredictable, and "slow response" often occurs. To find the true causes of "slow response", you need to print the log in every place where errors can occur and record each call. The cost is very high for doing so.
-   Insufficient monitoring
    -   Rapid business development and fast application iteration lead to frequent API changes of applications and increased dependencies. This further contributes to the deterioration of the quality of code. Applications need a comprehensive monitoring system that automatically monitors every API of the application and records abnormal calls.

## Solution

After being installed, the ARMS agent can use ARMS application monitoring features, such as thread profiling, trace diagnosis, API monitoring, to monitor all slow calls. This does not change the code of your application.

## Prerequisites

Make sure you have installed the ARMS agent for your applicartion.

## Step 1: View the statistics of slow SQLs

The installed ARMS agent collects and shows the application's total requests, average response time, count of errors, real-time instances, number of full garbage collection \(GC\) activities, slow SQLs, exceptions, and slow calls within the selected period. The agent also shows how these metrics change when compared with their counterparts in the previous day and previous week. Follow these steps to view the statistics of slow SQLs.

1.  In the left-side pane of the ARMS console, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, click the name of your application.

3.  On the Application Overview page, the total number of exceptions and how these changed from the previous day and previous week are displayed at the top of the Overview Analysis tab.

    In this example, there are 42 times of slow SQLs.


## Step 2: Find and locate slow APIs

On the Interface Invocation page, ARMS shows all APIs provided by the monitored application, and the number of calls and consumed time on this API. Slow APIs are marked to help you quickly locate them.

1.  Click **Interface Invocation** in the left-side pane of the ARMS console.

2.  In the **Interface Selection** section of the Interface Invocation page, select the slow API that is called the most frequently. View detailed information of the API on the right.

## Step 3: View and locate the problem code

After locating a slow API, you need to find the problem code to eliminate the problem. A snapshot is a complete record of an entire trace. The snapshot includes the code and time consumption of each call, and helps you precisely locate the problem code.

1.  Click the **Interface Snapshot** tab on the Interface Invocation page.

    On the Interface Snapshot tab, you can view snapshots of all APIs corresponding to this API.

2.  On the Interface Snapshot tab, click the TraceId of a trace, and then click the magnifier icon in the **Method Stack** column to view the problem code.

    To find the target trace, see [Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md).

    In this example, most of the time of this 705 ms call is spent in calling the SQL `SELECT * FROM l_employee`.


At this point, the causes for a specific slow call are revealed. This effectively helps you with the subsequent code optimization. You can also return to the Interface Invocation page to view other slow calls in the list and solve them one by one.

