# Slow session tracing

The slow session tracing function provides a performance waterfall chart for static resource loading during page loading. This helps you learn more about page resource loading status based on page performance data and quickly locate performance bottlenecks.

## Prerequisites

The browser monitoring SDK of Application Real-Time Monitoring Service \(ARMS\) does not report static resource information loaded on the page by default. To obtain information about static resources loaded on the page and enable slow session tracing, set SendResource to True in the `config` file of the SDK. After the application is redeployed, when an onload event on the page is triggered, the information about static resources loaded on the current page is reported. Then, you can quickly locate slow page loading problems in ARMS browser monitoring.

The SDK configuration is as follows:

```
<script>
!( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"atc889zkcf@8cc3f6354******",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?",sendResource:true};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>
```

**Note:** The reporting of static resource loading information is triggered during page onload, with a large amount of information reported. When the loading time is greater than 8s, the full report mode is used. If the loading time is within the range of 2s to 8s, 5% of the information is sampled and reported. If the loading time is less than 2s, no information is reported. We recommend that you do not set this parameter if your application requires high page performance.

## Portal

1.  In the left-side navigation pane, choose **Browser Monitoring**. On the **Browser Monitoring** page, find the target application and click the application name.
2.  In the left-side navigation pane, choose **Application** \> **Session Traces**.

## Use case: locate page performance bottlenecks

The following example shows how to locate page performance bottlenecks.

1.  In the left-side navigation pane, choose **Application** \> **Page Speed**. The result is shown in the following figure. It took 36.7s to completely load the page at 11:00.

    ![ARMS Browser Monitoring: Slow Session Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3092576751/p43617.png)

2.  On the Page Speed page, scroll down the page to the **Slow Page Session Trace \(Top 20\)** section. This section lists the top 20 sessions with the lowest page loading speed within the specified period of time.

    In the following figure, the page loading speed of a session at 11:36:46 is 36.72s. This access is the direct cause for the sharp increase in the page loading time.

    ![ARMS Browser Monitoring: Slow Sessions Top 20](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3092576751/p43619.png)

3.  In the **Page** column of the Slow Page Session Trace \(Top 20\) section, click a page name, and choose **Session Traces** \> **Session Details** from the shortcut menu. The **Page Resource Loading Waterfall** section displays the waterfall chart for page static resource loading. You can use this waterfall chart to quickly locate the performance bottlenecks for resource loading.

    ![ARMS Browser Monitoring: Page Resource Loading Waterfall](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43621.png)

4.  Choose **Session Traces** \> **Session Details**. In the **Page Information** section of the page that appears, you can view the client IP address, browser, operating system, and other information of the current access and locate the cause for slow session and optimize the page accordingly.

    ![ARMS Browser Monitoring: Page Information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43622.png)


## Other channels for detecting performance problems

In addition to the Page Speed page, you can also locate performance problems on the **Session Traces** page.

1.  In the left-side navigation pane, choose **Session Traces**. Then, you can view the list of all sessions of your application. You can filter sessions by page URL, session ID, browser, browser version, and other conditions.

    ![ARMS Browser Monitoring: Session Tracking - Sessions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5329230061/p43623.png)

2.  In the **Actions** column, click **Details**. The **Session Details** page appears, on which you can view the basic page information, page resource loading waterfall chart, and API loading waterfall chart.

## FAQ

1.  **Why is `Size` 0 on the resource loading waterfall chart?**

    `Size` is obtained by PerformanceResourceTiming.transferSize. The read-only attribute of transferSize indicates the size of the extracted resource in eight bits. If resources are obtained from the local cache or are cross-origin resources, the returned value of this parameter is 0.

    Open the Chrome browser, press **F12** to open the developer tool panel. When **Disable cache** on the **Network** tab is not selected, transferSize is 0.

    ![Disable Cache Disabled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43627.png)

    **Solution**

    Select **Disable cache**. Then, the actual value of `transferSize` is displayed.

    ![Disable Cache Enabled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43629.png)

    ![Transfersize Normal](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4092576751/p43630.png)

2.  **Why is `Time` 0 on the resource loading waterfall chart?**

    `Time` is obtained by PerformanceResourceTiming.duration. On the static resource loading waterfall chart, `Time` is sometimes 0. The reason is that the request hits a long cache that is controlled by `max-age`.

    **Solution**

    Open the Chrome browser and press **F12** to open the developer tool panel. Clear **Disable cache** on the **Network** tab and refresh the page. Then, the network access time is displayed.

3.  **Why is the returned value for Time 0?**

    The value of many time-related parameters returned by an API is 0. The reason is that the time point for obtaining the cross-origin resources is 0 due to the same-origin policy. The following attributes are involved:

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

    In the resource response header, add `Timing-Allow-Origin`, for example, `Timing-Allow-Origin:*`.

4.  **In which time range does the API loading waterfall chart show the API loading status?**

    The corresponding time range for API loading waterfall chart is as follows:

    -   Start time: the time when the page starts to load
    -   End time: full page loading time + 1 minute
    The API loading waterfall chart shows the overall status of the requested API during page loading.

5.  **Why is the response time on the API loading waterfall chart different from that on the page resource loading waterfall chart?**

    The response time on the API loading waterfall chart is several milliseconds longer than that on the page resource loading waterfall chart, because the two values are obtained in different ways. Specifically, the response time on the API loading waterfall chart is the time consumed from the API sending a request to the API returning the data. The API response time on the page resource loading waterfall chart is obtained by calling performance.getEntriesByType\('resource'\) provided by the browser.

    The several-millisecond difference does not affect the troubleshooting of performance bottlenecks.

6.  **What is the start time of the timeline on the API loading waterfall chart?**

    The timeline start time of the API loading waterfall chart is the difference between the time when the API sends a request and the time when the fetchStart value of the page is returned. This timeline displays when the API sends the request and its response time.


## More information

-   [Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)
-   [Browser monitoring FAQ](/intl.en-US/Browser monitoring/Browser monitoring FAQ.md)

