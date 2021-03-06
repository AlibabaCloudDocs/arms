# Page loading speed

This topic describes the page loading speed detection and analysis features in frontend monitoring of Application Real-Time Monitoring Service \(ARMS\).

After your application is connected to the ARMS frontend monitoring feature, you can view the following performance data of the application on the Page Speed page:

**Note:** You can manually report custom performance metrics, such as the first paint time and time to interact. For more information, see [performance\(\)](/intl.en-US/Browser Monitoring/API reference.md).

-   [Details of the page loading time](#section_w5n_wpq_gfb)
-   [Waterfall chart of page loading data](#page)
-   [Page performance distribution](#performance)
-   [Traces of slow page sessions](#Slowpage)
-   [Page loading distribution](#geographic)
-   [Custom performance metrics that are manually reported](/intl.en-US/Browser Monitoring/API reference.md)

## Go to the Page Speed page

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application that you want to view.
3.  In the left-side navigation pane, choose **Application** \> **Page Speed**.

In the **Page Speed** section, you can rank the pages by first paint time or page views \(PVs\), and change the display order by clicking the upward or downward arrow.

![Page Speed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43552.png)

## Details of the page loading time

![Page Load Time Details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43555.png)

**Note:**

-   In the Page Load Time Details section, the data in the curve chart is displayed based on the average values of the metrics within the specified time range. The average value reflects the average performance over a period of time. However, this value is sensitive to extreme values and large fluctuations. For example, if the overall page loading speed is slow due to weak network connection during an access request, the average response time is long. You can click the ![Filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6509242161/p67877.png) icon in the upper-right corner to remove extreme values. This way, the impact of extreme values on the overall performance trend is avoided.
-   If the data in the curve chart increases sharply, you can use the Performance Sample Distribution and Slow Page Session Trace\(TOP20\) sections to identify the issue.

## Waterfall chart of page loading data

In the Page Load Waterfall Plot section, the waterfall chart shows the response time in each stage based on the page loading order. Each type of data in the figure is the average value of a specified metric within a specified time range. To optimize performance, we recommend that you implement the related countermeasures on specific stages.

![Page Load Waterfall Plot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43557.png)

## Page performance distribution

The Performance Distribution section shows the distribution of the page performance.

On the **Performance Stacked Area Chart** tab, a stack line chart is displayed. This chart uses time as the horizontal axis. You can view the distribution of performance metrics at different points in time.

![Performance View](../images/p58838.png "Performance Stacked Area Chart tab")

On the **Performance Sample Distribution** tab, you can view the sample proportion of the page loading time in the specified time range. For example, you can view the number of pages that can be opened within 1 second and the proportion of samples of long-tail users.

![Performance Sample Distribution](../images/p43558.png "Performance Sample Distribution tab")

## Traces of slow page sessions

The Slow Page Session Trace\(TOP20\) section provides a performance waterfall chart of static resource loading during the page loading process. In this section, you can view the status of page resource loading based on page performance data. This allows you to identify and handle performance bottlenecks at the earliest opportunity. For more information, see [Session tracing](/intl.en-US/Browser Monitoring/Console functions/Session tracing.md).

![Slow Page Session Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2092576751/p43562.png)

## Page loading distribution

A page is loaded on the browser of a user. The loading time is determined by specific factors. These factors include the geographical location, network condition, browser, and carrier. Therefore, the frontend monitoring feature provides the statistics on geographical distribution, terminal distribution, network distribution, and version distribution. This allows you to identify performance bottlenecks.

![Geo View](../images/p43563.png "Geographical View section")

![Device View](../images/p43565.png "Terminal View section")

![Network View](../images/p58812.png "Network View section")

![Version View](../images/p58813.png "Version View section")

## Description of performance metrics

|Reported field|Description|Calculation method|Remarks|
|--------------|-----------|------------------|-------|
|First Meaningful Paint \(FMP\)|The First Meaningful Paint.|For more information, visit [Technical solution of FMP](https://zhuanlan.zhihu.com/p/44933789).|None|
|fpt|The FPT.|responseEnd - fetchStart|This field indicates the duration from the time when a request is initiated to the time when the browser begins to parse the bytes of the first batch of HTML documents.|
|tti|The time to interact \(TTI\).|domInteractive - fetchStart|This field indicates the time when the browser starts to load resources after it resolves all HTML documents and constructs the DOM.|
|ready|The time it takes to complete HTML loading, which is the time it takes to construct the DOM.|domContentLoadEventEnd - fetchStart|If a JavaScript \(JS\) script is executed synchronously on the page, the execution time of the JS script can be calculated based on the following formula: Execution time of the JS script = ready - tti.|
|load|The time it takes to completely load the page.|loadEventStart - fetchStart|This field can be calculated based on the following formula: load = fpt + dom + \(ready - tti\) + res.|
|firstbyte|The time it takes to generate the first response packet.|responseStart - domainLookupStart|None|

|Reported field|Description|Calculation method|Remarks|
|:------------:|:---------:|:----------------:|:-----:|
|dns|The amount of time consumed for DNS query.|domainLookupEnd - domainLookupStart|None|
|tcp|The amount of time consumed for TCP connection.|connectEnd - connectStart|None|
|ttfb|The time to first byte \(TTFB\), which indicates the amount of time it takes to respond to a request.|responseStart - requestStart|TTFB can be calculated in multiple ways. For more information about how TTFB is calculated in ARMS, visit [Google development definition](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference#timing).|
|trans|The amount of time consumed for data transmission.|responseEnd - responseStart|None|
|dom|The amount of time consumed for document object model \(DOM\) resolution.|domInteractive - responseEnd|None|
|res|The amount of time consumed for resource loading.|loadEventStart - domContentLoadedEventEnd|This field indicates the amount of time consumed for synchronously loading resources on the page.|
|ssl|The amount of time consumed for SSL connection.|connectEnd - secureConnectionStart|This field is valid only when HTTPS is used to transmit data.|

