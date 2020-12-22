# Diagnose errors on the server

It is challenging to analyze the causes of webpage errors, which are one of the most common problems of Internet applications. After being installed on an application, the Application Real-Time Monitoring Service \(ARMS\) agent can automatically capture, collect, count, and track exceptions without modifying the application code. You can use the agent to accurately locate all exceptions in the application and perform online diagnosis.

## Problem description

Webpage errors, frequently taking the form of a "5XX" error, are one of the most common problems for Internet applications. "5XX" errors usually occur on the server side. The server side has the most complex business logic and it is the most error-prone part of the entire network-request link. Errors on the server side prove to be the most challenging for cause analysis. O&M engineers or development engineers often have to log on to the target server to view logs and determine the causes.

For applications with less complex logic and short uptimes, logging on to the server to view logs can solve most of these problems. However, this method has been proven useless many times in the following scenarios.

-   When you want to know the time and frequency of a specific type of error in a distributed application cluster.
-   A system has been running for a long time, but you do not care about the residual exceptions. You just want to know about today's additional exceptions as compared with yesterday's, and additional exceptions after the release of the system compared with before the release of the system.
-   When you view the web requests and relevant parameters associated with an exception.
-   Customer Services provides the number of an order that the user fails to place for cause analysis of the failure.

## Solution

Install an ARMS agent on the application. The ARMS agent can automatically capture, collect, count, and track exceptions without modifying the application code. The agent presents a clear picture of various errors.

## Prerequisites

Make sure you have installed the ARMS agent for your application.

## Step 1: View statistics of application exceptions

The installed ARMS agent collects and shows the application's total requests, average response time, count of errors, real-time instances, number of full garbage collection \(GC\) activities, slow SQLs, exceptions, and slow calls within the selected period. The agent also shows how these metrics change when compared with their counterparts in the previous day and previous week. Follow these steps to view the statistics of application exceptions.

1.  In the left-side navigation pane of the ARMS console, choose **Application Monitoring** \> **Applications**.

2.  On the **Applications** page, click the name of your application.

3.  On the **Application Overview** page, the total number of exceptions and how it changes from the previous day and previous week are displayed at the top of the **Overview Analysis** tab.

4.  Scroll the page to the **Exception Type** section at the bottom of the **Overview Analysis** tab. Here you can view the number of times for which each type of exception occurs.

5.  In the left-side navigation pane, click **Application Details**, and then **Exception Analysis** on the right of the page. You can view exception statistics, error count, and exception details on this tab.


## Step 2: Diagnose the causes of the exception

The statistics of application exceptions are insufficient for locating the causes for exceptions. The abnormal stack in the log contains the code snippet for the call. However, it does not contain the complete upstream and downstream information and request parameters of this call. The ARMS agent's bytecode enhancement technology allows you to capture complete upstream and downstream call snapshots of exceptions at a low performance consumption. Then you can further identify the specific causes for the exceptions.

1.  On the **Exception Analysis** tab, click **Interface Snapshot** in the **Actions** column of a certain type of exception.

    Call trace related to this exception type is displayed on the **Interface Snapshot** tab.

2.  On the **Interface Snapshot** tab, click the TraceId of an incorrect call.

    To find the target trace, see [Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md) .

3.  On the page that appears, view the trace information of the target exception. Click the magnifier icon in the **Method Stack** column to view the detailed request parameters and exception log of the call. This allows you to retrieve the context information of the exception.


At this point, the causes for the exception are revealed. This effectively helps you with the subsequent code optimization. You can also return to the Interface Invocation page to view other exceptions in the list and solve them one by one.

