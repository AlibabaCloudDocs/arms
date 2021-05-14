# Diagnose slow page loading

Difficulties exist when you identify and troubleshoot the issue of slow page loading. To resolve this issue, the slow session tracing feature in frontend monitoring of Application Real-Time Monitoring Service \(ARMS\) provides a performance waterfall chart for static resource loading on pages. This allows you to check the resource loading status on the pages, identify the root cause, and troubleshoot the issue.

## Issue description

Slow page loading is one of the common and noted issues. You may encounter the following difficulties when you identify and troubleshoot the issues:

-   Difficult to replicate.

    For example, when User A visits a page, the page is loaded on the browser of User A. The page loading time is affected by factors such as the region, network, browser, and carrier. Therefore, the actual situation that occurred when User A accessed the page is difficult to be replicated.

-   Lack of monitoring information for in-depth investigation.

    Most frontend monitoring projects use the PerformanceTiming object to obtain the loading time of the full page, which excludes the loading time of static resources. Therefore, performance bottlenecks cannot be identified.


## Solution

You can connect the web application to ARMS frontend monitoring, enable the page resource reporting feature, and use the slow session tracing feature of ARMS frontend monitoring to identify the performance bottleneck.

## Step 1: Connect your application to ARMS frontend monitoring

By default, the ARMS frontend monitoring SDK does not report information about static resource loading. However, if you want to use the slow session tracing feature to identify the issue of slow page loading, the information about static resource loading is required.

For more information about how to connect your application to ARMS frontend monitoring, see [Install the browser monitoring probe by using CDN](/intl.en-US/Browser Monitoring/Quick start/For Web applications/Install the browser monitoring probe by using CDN.md).

**Note:** When you connect your application to ARMS frontend monitoring, you must select **Enable Page Resources Reporting** to enable slow session tracing.

## Step 2: Identify the issue

You can identify the issue by using one of the following methods:



1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Browser Monitoring**.
3.  On the Browser Monitoring page, click the name of the application that you want to view.
4.  In the left-side navigation pane, click **Page Speed**.

    For more information about the Page Speed page, see [Page loading speed](/intl.en-US/Browser Monitoring/Console functions/Page loading speed.md). In this example, the page performance is poor. The loading time of the full page reaches 36.7s at 11:00.

    ![Page Load Time Details section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6502601161/p47275.png)

5.  On the **Page Speed** page, drag the right-side scroll bar to go to the **Slow Page Session Trace \(TOP20\)** section.

    This section lists the top 20 sessions with the lowest page loading speed within the specified period of time.

    In this example, the page loading speed of a session reaches 36.72s at 11:36:46. This access is the direct cause of the sharp increase in the page loading time.

    ![Slow Page Session Trace (TOP20) section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6502601161/p47303.png)

6.  In the **Slow Page Session Trace\(TOP20\)** section, click the name of the relevant page in the **Page** column.

    The Slow Loading Details page appears.

7.  Identify the cause and troubleshoot the issue based on the information on the Slow Loading Details page.

    The **Page Information** section in the upper part of the Slow Loading Details page displays the access information such as the client IP address, browser, and operating system. This helps you further identify the cause of the issue.

    ![Slow Loading Details page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6502601161/p47306.png)

    The **Page Resource Loading Waterfall** section of the Slow Loading Details page displays a waterfall chart of static resource loading. This helps you identify the performance bottleneck.

    ![Page Resource Loading Waterfall section](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7502601161/p47304.png)

    For more information about the Slow Loading Details page, see [Slow session tracing](/intl.en-US/Browser Monitoring/Tutorials/Slow session tracing.md).


1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Browser Monitoring**.
3.  On the Browser Monitoring page, click the name of the application that you want to view.
4.  In the left-side navigation pane, click **Session Traces**.

    The Session List section displays all the sessions of the selected application. You can filter sessions by username, user ID, or session ID to identify time-consuming sessions.

5.  In the Session List section, click the name of the session that you want to view. Then, identify the cause and troubleshoot the issue based on the information on the Session Tracking Details page.

    For more information about the Session Traces page, see [Slow session tracing](/intl.en-US/Browser Monitoring/Tutorials/Slow session tracing.md).


The troubleshooting is complete by using the slow session tracing feature. This feature can help you replicate the page resource loading status and identify the performance bottleneck.

## What to do next

To prevent passive diagnostics after an exception occurs, you can also use the alert feature of ARMS to create an alert rule for a specific API or all APIs. This ensures that the O&M team receives a notification immediately after an exception occurs.

For more information about how to create an alert rule, see [Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md).

## References

-   [Page loading speed](/intl.en-US/Browser Monitoring/Console functions/Page loading speed.md)
-   [Slow session tracing](/intl.en-US/Browser Monitoring/Tutorials/Slow session tracing.md)
-   [Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md)

