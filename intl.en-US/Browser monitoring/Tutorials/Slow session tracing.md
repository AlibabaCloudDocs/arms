# Slow session tracing

The slow session tracing feature of Application Real-Time Monitoring Service \(ARMS\) provides a performance waterfall chart for static resource loading during page loading. This helps you learn more about the loading status of page resources based on page performance data and locate performance bottlenecks.

## Prerequisites

**Note:** The reporting of static resource loading information is triggered during page loading, and a large amount of information is reported. When the loading time is greater than 8s, full data is reported. If the loading time is within the range from 2s to 8s, 5% of the information is sampled and reported. If the loading time is less than 2s, no information is reported. We recommend that you do not set this parameter if your application requires high page performance.

By default, ARMS Browser Monitoring SDK does not report information about static resources loaded on a page. To obtain information about static resources loaded on a page and enable slow session tracing, set sendResource to true in the `config` file of the SDK. After the application is redeployed, when an onload event on the page is triggered, the information about static resources loaded on the current page is reported. Then, you can locate slow page loading problems in ARMS Browser Monitoring.

The following code shows an example of the SDK configuration:

```
<script>
!( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"atc889zkcf@8cc3f6354******",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?",sendResource:true};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>
```

## Portal

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of your application.
3.  In the left-side navigation pane, choose **Application** \> **Session Traces**.

## Use case: Locate page performance bottlenecks

The following example shows how to locate page performance bottlenecks.

1.  In the left-side navigation pane, choose **Application** \> **Page Speed**. The result is shown in the following figure. It took 36.7s to completely load the page at 11:00.

    ![ARMS Browser Monitoring: Slow Session Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3092576751/p43617.png)

2.  On the Page Speed page, scroll down the page to the **Slow Page Session Trace\(TOP20\)** section. This section lists the top 20 sessions with the lowest page loading speed within the specified period of time.

    To change the specified time period, you can click the clock icon in the upper-right corner of this section and select a value.

    In the following figure, the page loading speed of a session at 11:36:46 is 36.72s. This access is the direct cause of the sharp increase in the page loading time.

    ![ARMS Browser Monitoring: Slow Sessions Top 20](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3092576751/p43619.png)

3.  In the Slow Page Session Trace\(TOP20\) section, click a page name in the **Page** column to go to the **Trace Sessions** \> **Session Details** page. This page provides an intuitive view of the waterfall chart for the loading status of static page resources and allows you to locate the performance bottleneck for resource loading.

    ![ARMS Browser Monitoring: Page Resource Loading Waterfall](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43621.png)

4.  Choose **Session Traces** \> **Session Details**. On the page that appears, you can view the client IP address, browser, operating system, and other information of the current access in the **Page Information** section. Then, you can locate the causes of slow sessions and optimize the page accordingly.

    ![ARMS Browser Monitoring: Page Information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43622.png)


## Other channels for detecting performance problems

In addition to the Page Speed page, you can also locate performance problems on the **Session Traces** page.

1.  In the left-side navigation pane, choose **Session Traces**. On the **Session Traces** page, you can view the list of all sessions of your application. You can filter sessions based on conditions such as the username, user ID, page URL, session ID, browser, and browser version.

    ![ARMS Browser Monitoring: Session Tracking - Sessions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9502601161/p43623.png)

2.  In the **Session ID** column, click the ID of the session whose details you want to view. On the **Session Details** page, you can view the session overview and session traces. For more information, see [Session tracing](/intl.en-US/Browser monitoring/Console functions/Session tracing.md).

## FAQ

1.  **Why is `Size` 0 on the waterfall chart for resource loading?**

    `Size` is obtained by PerformanceResourceTiming.transferSize. The read-only attribute of transferSize indicates the size of the extracted resource in eight bits. If resources are obtained from the local cache or are cross-origin resources, the returned value of this parameter is 0.

    Open the Chrome browser, press **F12** to open the developer tool panel. When **Disable cache** on the **Network** tab is not selected, transferSize is 0.

    ![Disable Cache Disabled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9502601161/p43627.png)

    ![Transfersize 0](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0178342161/p43628.png)

    **Solution**

    Select **Disable cache**. Then, the actual value of `transferSize` is displayed.

    ![Disable Cache Enabled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43629.png)

    ![Transfersize Normal](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9502601161/p43630.png)

2.  **Why is `Time` 0 on the waterfall chart for resource loading?**

    `Time` is obtained by PerformanceResourceTiming.duration. On the waterfall chart for static resource loading, `Time` is sometimes 0. The reason is that the request hits a long cache that is controlled by `max-age`.

    **Solution**

    Open the Chrome browser and press **F12** to open the developer tool panel. Clear **Disable cache** on the **Network** tab and refresh the page. Then, the network access time is displayed.

3.  **Why is the returned value for Time 0?**

    The value of many time-related parameters returned by an API is 0. The reason is that the time point for obtaining cross-origin resources is 0 due to the same-origin policy. The following attributes are involved:

    -   redirectStart
    -   redirectEnd
    -   domainLookupStart
    -   domainLookupEnd
    -   connectStart
    -   connectEnd
    -   secureConnectionStart
    -   requestStart
    -   responseStart
    **Solution**

    Add `Timing-Allow-Origin`, such as `Timing-Allow-Origin:*`, to the resource response header.

4.  **In which time range does the waterfall chart for API loading show the API loading status?**

    The following information shows the start time and end time of the time range on the waterfall chart for API loading:

    -   Start time: the time when the page starts to load
    -   End time: full page loading time plus 1 minute
    The waterfall chart for API loading shows the overall status of the requested API during page loading.

5.  **Why is the response time on the waterfall chart for API loading different from that on the waterfall chart for page resource loading?**

    The response time on the waterfall chart for API loading is several milliseconds longer than that on the waterfall chart for page resource loading, because the two values are obtained in different ways. The response time on the waterfall chart for API loading is calculated from the time when the API sends a request to the time when the API returns data. The API response time on the waterfall chart for page resource loading is obtained by calling performance.getEntriesByType\('resource'\) that is provided by the browser.

    The several-millisecond difference does not affect the troubleshooting of performance bottlenecks.

6.  **What is the start time of the timeline on the waterfall chart for API loading?**

    The start time of the timeline on the waterfall chart for API loading is the difference between the time when the API sends a request and the time when the fetchStart value of the page is returned. This timeline displays when the API sends the request during page loading and its response time.


## References

-   [Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)
-   [Browser monitoring FAQ](/intl.en-US/Browser monitoring/Browser monitoring FAQ.md)

