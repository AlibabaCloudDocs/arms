# Diagnose slow page loading

Difficulties exist when you identify and troubleshoot the problem of slow page loading. To solve this problem, the slow session tracing feature in browser monitoring of Application Real-Time Monitoring Service \(ARMS\) provides a performance waterfall chart for static resource loading on pages. This allows you to check the resource loading status on the pages, identify the root cause, and troubleshoot the problem.

## Problem description

Slow page loading is one of the common and noted problems for users. You may encounter the following difficulties when you identify and troubleshoot the problems:

-   Difficult to reproduce problems

    For example, when user A accesses a page, the page is loaded in the local browser of user A. The actual situation where user A accesses the page cannot be reproduced because the page loading time is affected by factors such as the region, network, browser, or carrier.

-   Lack of monitoring information for troubleshooting

    Most browser monitoring services use the PerformanceTiming object to obtain all information about page loading time, which does not include static resource loading time. Therefore, performance bottlenecks cannot be identified.


## Solution

You can connect the web application to ARMS browser monitoring, enable the page resource reporting feature, and use the slow session tracing feature of ARMS browser monitoring to identify the performance bottleneck.

## Step 1: Connect to ARMS browser monitoring

By default, the ARMS browser monitoring SDK does not report static resource loading information. However, if you want to use the slow session tracing feature to identify the slow page loading problem, the static resource loading information is required.

Connect your web application to ARMS browser monitoring. For more information, see [Install the browser monitoring probe by using CDN](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For Web applications/Install the browser monitoring probe by using CDN.md).

**Notice:** When you connect the web application to ARMS browser monitoring, you must select **Enable Page Resources Reporting**.

## Step 2: Identify the problem

You can identify the problem by using one of the following methods:

**Method 1: Check the access speed**

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home).In the left-side navigation pane, click **Browser Monitoring**.

2.  On the Browser Monitoring page, click the name of your application.

3.  In the left-side navigation pane, click **Page Speed**.

    For more information about the Page Speed page, see [Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md). In this example, the page performance is poor. The loading time of the full page reaches 36.7s at about 11:00.

4.  On the **Page Speed** page, drag the right-side scroll bar to view the **Slow Page Session Trace \(TOP20\)** section. This section lists top 20 sessions with the lowest page loading speed within the specified time range.

    In this example, the page loading time at 11:36:46 is 36.72s, which causes a sharp increase of the page loading time.

5.  In the **Slow Page Session Trace \(TOP20\)** section, click the page name in the **Page** column to access the Session Details page. Then, identify the cause and troubleshoot the problem based on the information on the Session Details page.

    The **Page Information** section in the upper part of the Session Details page shows the access information such as the client IP address, browser, and operating system. This helps you further identify the cause of the problem.

    The **Page Resource Loading Waterfall** section on the Session Details page shows the waterfall chart of static resource loading. This helps you identify the performance bottleneck.

    For more information about the Session Traces page, see [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).


**Method 2: Trace the session**

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home).In the left-side navigation pane, click **Browser Monitoring**.

2.  On the Browser Monitoring page, click the name of your application.

3.  In the left-side navigation pane, click **Session Traces** to access the Session List page.

    The Session List page shows the top 100 sessions of the application by loading time. You can filter sessions by page, session ID, browser, or browser version to identify time-consuming sessions.

4.  On the Session List page, find the session and click **Details** in the **Operation** column. Then, identify the cause and troubleshoot the problem based on the information on the Session Details page.

    For more information about the Session Traces page, see [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).


The troubleshooting is complete by using the slow session tracing feature. This feature can help you reproduce the page resource loading status and identify the performance bottleneck.

## What to do next

To avoid passive diagnostics after an exception occurs, you can also use the alert feature of ARMS to create an alert for one or all API operations. This ensures that the O&M team immediately receives a notification when an exception occurs.

For information about how to create an alert, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

## References

-   [Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)
-   [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md)
-   [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

