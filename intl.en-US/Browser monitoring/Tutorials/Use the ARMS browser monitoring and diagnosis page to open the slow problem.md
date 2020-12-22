# Use the ARMS browser monitoring and diagnosis page to open the slow problem

Page performance has an extremely impact on user experience, and user experience largely determines whether users stay. Therefore, frontend performance monitoring and analysis become particularly important. This topic describes how to use ARMS browser monitoring to diagnose slow page opening.

[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

## Advantages of ARMS browser monitoring

-   Multidimensional performance analysis based on real user data:
    -   Real user operations are completely restored without simulation or logon.
    -   Real user data truly reflects the end user experience, reduces statistical errors, and quickly determines the scope of user problems, such as which region, which device, and which browser.
-   Page performance analysis:
    -   First rendering Time: whether the time consumed by DNS resolution and TCP connection is high.
    -   DOM Ready time: whether the Request and Response time is high.
    -   Resource loading time: indicates whether resource loading is slow.
-   JS error analysis:

    Monitor and diagnose JS errors.

-   Custom statistics:

    You can use the SDK to report custom events for custom statistics.

-   Access details:

    You can query the access information of all the monitored users.

-   Interconnection with application monitoring request data:

    After confirming that the page loading is slow, you can coordinate with application monitoring for troubleshooting.


## Procedure

The following is an example of a troubleshooting policy.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose**Browser monitoring**, In**Browser monitoring**Click the name of your application. In the left-side navigation pane, choose**Application** \> **Access speed**.

3.  In**Page loading time details**Region and**Page loading waterfall chart**Check whether the key performance metrics are abnormal.

    1.  If the first rendering time is too high, or the time consumed by DNS query, TCP connection, and SSL connection is too high, it means that the slow page opening may be caused by network reasons, so you need to check your network problems.

    2.  If the DOM Ready time is too high, or the request response and content transmission time is too high, the reason for slow page opening may be that the API request is slow, then you need to perform the step[4](#step_3wg_h3c_tuk)For troubleshooting.

    3.  If the page full loading time is high, or the DOM parsing and resource loading time is high, the reason for the slow page opening may be that the front-end resource loading is slow, then you need to perform the step[5](#step_u9x_dal_d20)For troubleshooting.

4.  In the left-side navigation pane, choose**Application** \> **API details**.

    1.  In**API request list**Region and click an API**Slow Times**The number of columns.

    2.  In the API slow count details dialog box that appears, click**Network request information**In the upper-right corner of the area,**Redirect call link**To view the overall RT of the browser monitoring and the call sequence diagram of the backend application.

        -   If the backend application processing time is short but the overall time consumption is long, it indicates that the network transmission of API requests from sending to the server and from returning data from the server to the browser is long. In the left-side navigation pane, choose**Application** \> **Access details**, And then click**API logs**, Set the preceding API to the search value, and then click**Search**To view the network, region, browser, device, and operating system of this access.
        -   If the backend application takes a long time to process, the backend processing performance is poor. Click**Method stack**Click the magnifier icon.**Local method stack**In the dialog box, check which part of the backend link is time-consuming and locate the problem.
5.  In**Slow session tracking \(top 20\)**Area and click the page name of a slow session.

    InSession DetailsPage, you can**Page resource loading waterfall chart**To view the details of resources that slow down the page.


[Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)

[Diagnose JS errors by using ARMS browser monitoring](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md)

