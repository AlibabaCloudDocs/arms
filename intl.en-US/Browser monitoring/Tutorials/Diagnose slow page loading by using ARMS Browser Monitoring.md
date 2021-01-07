# Diagnose slow page loading by using ARMS Browser Monitoring

Slow page loading extremely affects the user experience, which determines the user loyalty. Therefore, the browser performance monitoring and analysis is particularly important. This topic describes how to use Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring to diagnose slow page loading.

Your browser application has been connected to ARMS. For more information, see [Browser monitoring overview](/intl.en-US/Browser monitoring/Get started with browser monitoring/Browser monitoring overview.md).

## Issues that can be solved by ARMS Browser Monitoring

-   Multidimensional performance analysis based on real user data
    -   Fully restores real user operations without simulation and logon.
    -   Uses real user data to reflect the user experience, which reduces statistical errors and helps you determine the error location, such as the region, device, and browser.
-   Page performance analysis
    -   First Paint Time: specifies whether the Domain Name System \(DNS\) resolution time and the TCP connection time are long.
    -   DOM Ready: specifies whether the response time \(RT\) is long.
    -   Fully Loaded Time: specifies whether resource loading is slow.
-   JS error analysis

    Monitors and diagnoses JS errors.

-   Custom statistics

    Uses the software development kit \(SDK\) to report custom events for custom statistics.

-   Access details

    Queries all monitored user access information.

-   Integration with data on Application Monitoring

    Diagnoses slow page loading with Application Monitoring.


## Diagnose slow page loading

The following example shows the troubleshooting procedure:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the target application. In the left-side navigation pane, choose **Application** \> **Page Speed**.

3.  In the **Page Load Time Details** and **Page Load Waterfall Plot** sections, check whether key performance metrics are normal.

    -   If the value of First Paint Time in the Page Load Time Details section or the values of DNS Lookup, TCP Connection, and SSL Connection in the Page Load Waterfall Plot section are large, slow page loading may be caused by the network. In this case, check the network.
    -   If the value of DOM Ready in the Page Load Time Details section or the values of Time to First Byte\(TTFB\) and Content Download in the Page Load Waterfall Plot section are large, slow page loading may be caused by slow API responses. In this case, perform [Step 4](#step_3wg_h3c_tuk) to diagnose the issue.
    -   If the value of Fully Loaded Time in the Page Load Time Details section or the values of DOM Ready and Resource Download in the Page Load Waterfall Plot section are large, slow page loading may be caused by slow loading of browser resources. In this case, perform [Step 5](#step_u9x_dal_d20) to diagnose the issue.
4.  In the left-side navigation pane, choose **Application** \> **API Details**.

    1.  In the **API Requests** section, find the target API and click the number in the **Slow Responses** column.

    2.  In the API Slow Calls Details dialog box, click **Show Invocation Trace** in the upper-right corner of the **Network Request Information** section to view the overall RT of the browser and the call sequence diagram of the backend application.

        -   If the processing time of the backend application is short but the overall RT is long, the time consumed from API request sending to the server to data returning to the browser is long. In this case, choose **Application** \> **View Details** in the left-side navigation pane. On the page that appears, click the **API Logs** tab, set the preceding API as the search value, and then click **Search** to view the access information, such as the network, region, browser, device, and operating system.
        -   If the backend application takes a long time to process, the backend processing performance is poor. Click the magnifier icon in the **Method Stack** column. In the **Local Method Stack** dialog box, check which part of backend tracing is time-consuming to locate the problem.
5.  In the **Slow Page Session Trace\(TOP20\)** section, click the page name of a slow session.

    In the **Page Resource Loading Waterfall** section on the Slow Loading Details page, you can view the details of the resources that cause slow page loading.


## References

-   [Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)
-   [Diagnose JS errors by using ARMS browser monitoring](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md)

