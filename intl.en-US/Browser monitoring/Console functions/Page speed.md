# Page speed

This topic describes the functions on the Page Speed page of browser monitoring of Application Real-Time Monitoring Service \(ARMS\).

After connecting your application to ARMS browser monitoring, you can view the following performance data of your application on the Page Speed page:

-   [Page loading details](#section_w5n_wpq_gfb)
-   [Page loading waterfall chart](#page)
-   [Performance distribution](#performance)
-   [Slow page session tracing](#Slowpage)
-   [Page loading distribution](#geographic)

In the **Page Speed Ranking** section, you can rank the pages by first paint time or PV and click the upward or downward arrow to change the display order.

![Page Speed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43552.png)

## Page loading details

This module displays the following metrics.

-   Key performance metrics

-   First Paint Time

-   First Meaningful Paint

-   Time to First Interaction

-   DOM Ready

-   Fully Loaded Time

-   Page load time by intervals:

-   DNS Lookup

-   TCP Connection Time

-   Time to First Byte\(TTFB\)

-   Content Download

-   DOM Parsing

-   Resource Download


For more information about how these metrics are calculated, see [Statistical metrics](/intl.en-US/Browser monitoring/Statistical metrics.md).

![Page Load Time Details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43555.png)

**Note:**

-   The data in the line chart is displayed based on the average value of the metric within the specified time range. The average value reflects the average performance over a period of time, but is vulnerable to extreme values. For example, the overall page loading is very slow due to poor network connection during an access, and therefore the average response time is high. You can click the Filter icon in the upper-right corner to remove extreme values. In this way, the impact of extreme values on the overall performance trend is removed.
-   If the data in the line chart increases sharply, you can use the performance sample distribution and slow page session trace functions to locate the problem.

## Page loading waterfall chart

The waterfall chart visually shows the response time in each stage based on the page loading order. The data in the figure is the average value of a specified metric within a specified time range. To optimize performance, implement targeted measures at specific stages.

![Page Load Waterfall Plot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1092576751/p43557.png)

## Performance distribution

This module visually shows the page performance distribution.

On the **Performance Stacked Area Chart** tab, a stack line chart with time as the horizontal axis appears. You can view the distribution of performance at different time points.

On the **Performance Sample Distribution** tab, you can view the sample proportion of the page loading time in the specified time range. For example, how many pages can be opened within 1 second, or the proportion of samples of users with long tails.

![Performance Sample Distribution](../images/p43558.png "Performance sample distribution")

## Slow page session tracing

The slow session tracing function provides a performance waterfall chart for static resource loading during page loading. This helps you learn more about page resource loading status based on page performance data, and quickly locate performance bottlenecks. For more information, see [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).

![Slow Page Session Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2092576751/p43562.png)

## Page loading distribution

A page is loaded on the browser of the user. The loading time is related to factors such as the geographical location, network condition, browser, or carrier. Therefore, we provide statistics by factors such as geographical distribution, terminal distribution, network distribution, and version distribution to help you better locate performance bottlenecks.

![Geo View](../images/p43563.png "Geographical view")

![Device View](../images/p43565.png "Terminal view")

