---
keyword: [frontend monitoring, metric, FirstByte, FPT, TTI, log field]
---

# Statistical metrics

This topic describes the key statistical metrics on each page in frontend monitoring of Application Real-Time Monitoring Service \(ARMS\) and the fields in ARMS frontend monitoring logs.

## Satisfaction

[Application Performance Index](http://www.apdex.org/) \(APDEX\) is a global standard for evaluating application performance. The user experience of an application can be evaluated based on APDEX by three levels:

-   Satisfied \(0 to T\)
-   Tolerating \(T to 4T\)
-   Frustrated \(greater than 4T\)

The following formula is used to calculate the APDEX score:

```
APDEX score = (Number of satisfied samples + Number of tolerating samples/2)/Number of total samples
```

![Apdex](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4192576751/p43776.gif)

The preceding image is obtained from [apdex.org](http://www.apdex.org/images/overview_figure1_performancezones_256_111.gif).

The First Paint Time \(FPT\) is used as the metric to evaluate the APDEX of ARMS. The default value of T is 2 in seconds.

## JS stability

In ARMS, JavaScript \(JS\) stability is evaluated by the JS error rate of pages.

If an JS error occurs in a page view \(PV\) cycle, this PV cycle is considered as an error sample.

```
Error rate = Number of error samples/Number of total samples
```

In addition to the JS errors that are automatically reported, page exceptions also include errors reported when you manually call methods described in [API reference](/intl.en-US/Browser Monitoring/API reference.md).

## Access speed

In ARMS, access speed is evaluated by the FPT of a page.

All performance or speed statistics are collected by using the [Navigation Timing API](https://www.w3.org/TR/navigation-timing/) defined by the World Wide Web Consortium \(W3C\).

![Navigation Timing API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4192576751/p43777.png)

The preceding image is obtained from [www.w3.org](https://www.w3.org/TR/navigation-timing/#processing-model).

|Reported field|Description|Calculation method|Remarks|
|--------------|-----------|------------------|-------|
|FMP|The First Meaningful Paint \(FMP\).|For more information, see [Technical solution of FMP](https://zhuanlan.zhihu.com/p/44933789).|N/A|
|FPT|The FPT.|responseEnd - fetchStart|This field indicates the duration from the point in time when a request is initiated to the point in time when the browser begins to parse the bytes of the first batch of HTML documents.|
|TTI|The time to interact \(TTI\).|domInteractive - fetchStart|This field indicates the point in time when the browser starts to load resources after it resolves all HTML documents and constructs the document object model \(DOM\).|
|Ready|The time consumed to complete HTML loading, which is the time consumed to construct the DOM.|domContentLoadEventEnd - fetchStart|If a JS script is synchronously executed on the page, the execution time of the JS script can be calculated based on the following formula: Execution time of the JS script = Ready - TTI.|
|Load|The time consumed to completely load the page.|loadEventStart - fetchStart|This field can be calculated based on the following formula: Load = FPT + DOM + \(Ready - TTI\) + Res.|
|FirstByte|The time consumed to generate the first response packet.|responseStart - domainLookupStart|N/A|

|Reported field|Description|Calculation method|Remarks|
|:------------:|:---------:|:----------------:|:-----:|
|DNS|The time consumed for Domain Name System \(DNS\) query.|domainLookupEnd - domainLookupStart|N/A|
|TCP|The time consumed for Transmission Control Protocol \(TCP\) connection.|connectEnd - connectStart|N/A|
|TTFB|The time to first byte \(TTFB\), which indicates the time consumed to respond to a request.|responseStart - requestStart|TTFB can be calculated in different ways. For more information about how TTFB is calculated in ARMS, see [Google development definition](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference#timing).|
|Trans|The time consumed for data transmission.|responseEnd - responseStart|N/A|
|DOM|The time consumed for DOM resolution.|domInteractive - responseEnd|N/A|
|Res|The time consumed for resource loading.|loadEventStart - domContentLoadedEventEnd|This field indicates the time consumed to synchronously load resources on the page.|
|SSL|The time consumed for Secure Sockets Layer \(SSL\) connection.|connectEnd - secureConnectionStart|This field is valid only when HTTPS is used to transmit data.|

|Reported field|Description|Calculation method|Remarks|
|--------------|-----------|------------------|-------|
|FPT|The FPT.|onShow \(first page\) - onLaunch \(app\)|This field indicates the duration from the point in time when the mini program calls the onLaunch method to the point in time when the mini program calls the onShow method to display the first page.|

## Success rate of API calls

```
Success rate of API calls = Number of successful API calling samples/Number of total API calling samples
```

In addition to the AJAX requests that are automatically reported, samples for calculating the success rate of API calls also include the data reported when you manually call the methods described in [API reference](/intl.en-US/Browser Monitoring/API reference.md).

## Log fields

The following tables describe the fields included in ARMS logs.

|Field|Description|
|-----|-----------|
|uid|The ID of the user. The value is an identifier of the user and can be used to search for the user. You can specify a custom value. If you do not set this field, the SDK automatically assigns an ID to the user and updates the ID every six months.|
|username|The username. The SDK does not automatically assign a username to the user. If you do not set this field, it is left empty.|
|release|The version of the application.|
|environment|The production environment.|
|page|The page.|
|sampling|The sampling rate.|
|tag|The custom tag.|

|Field|Description|
|-----|-----------|
|api|The URL of the API call without parameters.|
|msg|The response string to the API call.|
|code|The HTTP status code.|
|time|The time consumed by the API.|
|success|Indicates whether the API call is successful.|

|Field|Description|
|-----|-----------|
|msg|The error message.|
|stack|The stack where the error occurs.|
|cate|The error type.|
|file|The file where the error occurs.|
|line|The line where the error occurs.|
|col|The column where the error occurs.|
|times|The number of times the error occurs.|

## Log overview

|Log type|Log field|Query field\(Common metric fields can be used to query or filter all types of logs\) |
|--------|---------|--------------------------------------------------------------------------------------|
|PV log|PV|-   PV
-   UV |
|Performance log|Perf|[Performance metrics](#section_hjl_zhr_s2b)|
|Slow loading log\(Performance logs in which the loading time is longer than 8 seconds\)

|RES|[Performance metrics](#section_hjl_zhr_s2b)|
|JS error log|Error|-   The JS error message
-   The URL of the JS error file
-   The JS error type |
|API log|API|-   The API name
-   The message returned by the API call
-   The HTTP status code
-   The time consumed by the API.
-   The domain name involved in the API call
-   Whether the API call is successful
-   Trace ID |
|SUM log|SUM|Custom key: event name \(example: scroll-count\)|
|AVG log|AVG|Custom key: event name \(example: scroll-time\)|
|Resource error log|ResourceError|The resource error|
|N/A|Custom|N/A|

