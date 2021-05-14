# Diagnose slow page loading by using the ARMS frontend monitoring feature

Slow page loading extremely affects the user experience, which determines the user loyalty. Therefore, frontend performance monitoring and analysis are particularly important. This topic describes how to use the Application Real-Time Monitoring Service \(ARMS\) frontend monitoring feature to diagnose slow page loading.

Your application is monitored by the ARMS frontend monitoring feature. For more information, see [Browser monitoring overview](/intl.en-US/Browser Monitoring/Quick start/Browser monitoring overview.md).

## Diagnose slow page loading

The following example shows the troubleshooting procedure:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**.

3.  On the **Browser Monitoring** page, click the name of the application that you want to view.

4.  In the left-side navigation pane, choose **Application** \> **Page Speed**.

5.  In the **Page Load Time Details** and **Page Load Waterfall Plot** sections, check whether the values of key performance metrics are normal.

    ![Page Load Time Details section](../images/p103086.png "Page Load Time Details section")

    ![Page Load Waterfall Plot section](../images/p103087.png "Page Load Waterfall Plot section")

    -   If the value of the First Paint Time parameter in the Page Load Time Details section or the values of the DNS Lookup, TCP Connection, and SSL Connection parameters in the Page Load Waterfall Plot section are large, slow page loading may be caused by the network. In this case, check the network.
    -   If the value of the DOM Ready parameter in the Page Load Time Details section or the values of the Time to First Byte\(TTFB\) and Content Download parameters in the Page Load Waterfall Plot section are large, slow page loading may be caused by slow API requests. In this case, perform [Step 4](#step_3wg_h3c_tuk) to diagnose the issue.
    -   If the value of the Fully Loaded Time parameter in the Page Load Time Details section or the values of the DOM Parsing and Resource Download parameters in the Page Load Waterfall Plot section are large, slow page loading may be caused by slow loading of frontend resources. In this case, perform [Step 5](#step_u9x_dal_d20) to diagnose the issue.
6.  In the left-side navigation pane, choose **Application** \> **API Details**.

    1.  On the **API Requests** tab, find the API that you want to view and click **Analyze** in the **Operation** column.

        ![API Request List](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3502601161/p111612.png)

    2.  On the API Details tab, click **Show Invocation Trace** in the upper-right corner of the **Request Details** section to view the overall response time of the frontend and the call sequence diagram of the backend application.

        ![Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4390839061/p111615.png)

        -   If the processing time of the backend application is short but the overall response time is long, the time consumed from API request sending to the server to data returning to the frontend is long. In this case, click **View Session** in the upper-right corner of the **Request Details** section of the API Details tab. Then, view the access information, such as the network connection type, region, browser, device, and operating system.
        -   If the backend application takes a long time to process the access request, the backend processing performance is poor. In this case, click the magnifier icon in the **Details** column. In the **Details** dialog box, check which part of backend tracing is time-consuming to locate the issue.
7.  In the left-side navigation pane, choose **Application** \> **Page Speed**.

8.  In the **Slow Page Session Trace\(TOP20\)** section of the Page Speed page, click the page name of a slow session.

    ![Slow Page Session Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4390839061/p111617.png)

    In the **Page Resource Loading Waterfall** section of the Session Traces page, you can view the details of the resources that cause slow page loading.


## References

-   [Page loading speed](/intl.en-US/Browser Monitoring/Console functions/Page loading speed.md)
-   [Diagnose JS errors by using ARMS browser monitoring](/intl.en-US/Browser Monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md)

