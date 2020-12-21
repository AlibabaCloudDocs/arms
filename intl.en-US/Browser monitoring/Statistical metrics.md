---
keyword: [Browser monitoring, Metric, firstbyte, fpt, tti, Log field]
---

# Statistical metrics

This topic describes the key statistical metrics on each page in application monitoring of Application Real-Time Monitoring Service \(ARMS\) and the fields in ARMS application monitoring logs.

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

The First Paint Time \(FPT\) is used as the metric to evaluate the APDEX of ARMS. The default value of T is 2 seconds.

## JS stability

In ARMS, JS stability is evaluated by the JS error rate of pages.

If any JS error occurs in a page view \(PV\) cycle, this PV cycle is considered as an error sample.

```
Error rate = Number of error samples/Number of total samples
```

In addition to the JS errors that are automatically reported, page exceptions also include errors reported when you manually call methods described in [API reference](/intl.en-US/Browser monitoring/API reference.md).

## Access speed

In ARMS, access speed is evaluated by the FPT of a page.

All performance or speed statistics are collected by using the [Navigation Timing API](https://www.w3.org/TR/navigation-timing/) defined by the World Wide Web Consortium \(W3C\).

![Navigation Timing API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4192576751/p43777.png)

The preceding image is obtained from [www.w3.org](https://www.w3.org/TR/navigation-timing/#processing-model).

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

|Reported field|Description|Calculation method|Remarks|
|--------------|-----------|------------------|-------|
|fpt|The FPT.|onShow \(first page\) - onLaunch \(app\)|This field indicates the duration from the time when the mini program calls the onLaunch method to the time when the mini program calls the onShow method to display the first page.|

## API call success rate

```
API call success rate = Number of successful API calling samples/Number of total API calling samples
```

In addition to the AJAX requests that are automatically reported, samples for API call success rate statistics also include the data reported when you manually call the methods described in [API reference](/intl.en-US/Browser monitoring/API reference.md).

## Log fields

The following tables describe the fields included in ARMS logs.

|Field|Description|
|-----|-----------|
|uid|The user ID.|
|username|The user name.|
|release|The version of the application.|
|environment|The production environment.|
|page|The page.|
|sampling|The sampling rate.|
|tag|The custom tag.|

|Field|Description|
|-----|-----------|
|api|The URL of the API request without parameters.|
|msg|The responseText, which indicates the response string to the API request.|
|code|The HTTP status code.|
|time|The time consumed by the API operation.|
|success|Indicates whether the API request is successful.|

|Field|Description|
|-----|-----------|
|msg|The error message.|
|stack|The stack where the error occurs.|
|cate|The error type.|
|file|The file where the error occurs.|
|line|The line where the error occurs.|
|col|The column where the error occurs.|
|times|The number for which the error occurs.|

## Log overview

|Log type|Type|Query field\(Common metric fields can be used to query or filter all types of logs\) |
|--------|----|--------------------------------------------------------------------------------------|
|PV log|PV|-   PV
-   UV |
|Performance log|Perf|[Performance metrics](#section_hjl_zhr_s2b)|
|Slow loading log\(Performance logs in which the loading time is longer than 8 seconds\)

|RES|[Performance metrics](#section_hjl_zhr_s2b)|
|JS error log|Error|-   The JS error message
-   The URL of the JS error file
-   The JS error type |
|API log|API|-   The API name
-   The API message
-   The HTTP status code
-   The time consumed by the API operation
-   The domain name of the API operation
-   Whether the API operation is successful
-   TraceID |
|SUM log|SUM|Custom key: event name \(example: scroll-count\)|
|AVG log|AVG|Custom key: event name \(example: scroll-time\)|
|Resource error log|ResourceError|The resource error|
|None|Custom|None|

