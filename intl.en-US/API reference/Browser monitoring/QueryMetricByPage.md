# QueryMetricByPage

Queries the metrics of Browser Monitoring.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=QueryMetricByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryMetricByPage|The operation that you want to perform. Set the value to `QueryMetricByPage`. |
|EndTime|Long|Yes|1596183532000|The end of the time range to query. Unit: milliseconds. |
|IntervalInSec|Integer|Yes|60000|The time interval between the data shards to be queried. Unit: milliseconds. Minimum value: 60,000. |
|Measures.N|RepeatList|Yes|pv|The measurement data of the metric. For more information, see [Queryable Browser Monitoring metrics](#section_2wv_zz8_zw7). You can add a maximum of five measurement data entries. |
|Metric|String|Yes|webstat.index|The metrics that you want to query. You cannot query custom metrics. For more information, see [Queryable Browser Monitoring metrics](#section_2wv_zz8_zw7). |
|StartTime|Long|Yes|1595319532000|The beginning of the time range to query. Unit: milliseconds. |
|OrderBy|String|No|rpc|The measurement data entry by which metrics are sorted. You can set this parameter to a type of measurement data. |
|Filters.N.Key|String|Yes|pid|The parameter of the filter condition for the query. The `pid` and `regionId` parameters are required. For information about how to obtain the `PID`, see [Obtain the PID of an application](#section_n8m_h9o_ebe). |
|Filters.N.Value|String|Yes|xxx@74xxx|The value of the filter condition for the query. The `pid` and `regionId` parameters are required. For information about how to obtain the `PID`, see [Obtain the PID of an application](#section_n8m_h9o_ebe). |
|Dimensions.N|RepeatList|No|\["detector\_browser","detector\_device"\]|The dimension by which metrics are queried. For more information, see [Queryable Browser Monitoring metrics](#section_2wv_zz8_zw7). You can add a maximum of five dimensions. |
|Order|String|No|ASC|The dimension by which metrics are sorted. Valid values:

-   `ASC`: ascending order
-   `DESC`: descending order |
|RegionId|String|No|cn-hangzhou|The ID of the region. |
|CurrentPage|Integer|No|1|Optional. The number of the page to return. Default value: `1`. |
|PageSize|Integer|No|10|The number of entries to return on each page. |

## Obtain the PID of an application

Log on to the Application Real-Time Monitoring Service \(ARMS\) console.In the left-side navigation pane, click **Browser Monitoring**. On the **Browser Monitoring** page, click the name of the application that you want to query to go to the overview page of this application.

The URL in the browser address bar contains the PID of this application in the format of `pid=xxx`. The browser is encoded. Therefore, you must modify the PID of applications. For example, if the PID in the URL is `xxx%4074xxx`, you must replace `%40` with `@`. The PID is modified to `xxx@74xxx`.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|200|The status of the API. Valid values:

-   2XX: successful
-   3XX: retried
-   4XX: request error
-   5XX: server error |
|Data|Struct| |The returned data struct. |
|Items|List|\[\]|The list of returned data structs. |
|Page|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|Total|Integer|0|The sum of queries. |
|Message|String|message|The returned message. |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the query was successful. Valid values:

-   `true`: successful
-   `false`: failed |

## Queryable Browser Monitoring metrics

You can call the QueryMetric operation to query the following metrics of Browser Monitoring.

**Note:**

-   You must set the `pid` and `regionId` parameters in the filters parameter.
-   If you have obtained the values of the pid and regionId parameters, add the values to the filters parameter to define the range of query results. If you have not obtained the values of the pid and regionId parameters, add the dimensions in the following table to the dimensions parameter to obtain a list of all possible values.

|Metric|Description|Dimension|Measurement data|
|------|-----------|---------|----------------|
|webstat.api|Success rate of API calls|-   api: the API request address without parameters
-   detector\_app\_version: the client version
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   release: the application version number
-   sr: the screen resolution

|-   count: the number of requests
-   rate: the success rate of API calls
-   avg\_time: the average response time |
|webstat.api.detail|API details|-   api: the API request address without parameters
-   ct: the network connection type
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   domain: the domain name
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_isp: the carrier
-   ip\_region\_id: the ID of a country or region outside China
-   msg: the returned message
-   page: the URL of the page
-   sr: the screen resolution

|-   count: the number of requests
-   fail\_count: the number of failed API calls
-   fail\_time: the response time for failed API calls
-   fail\_uv: the number of users who fail to call the API
-   success\_count: the number of successful API calls
-   success\_rate: the success rate
-   success\_time: the response time for successful API calls |
|webstat.apicost|Response time for successful API calls|-   api: the API request address without parameters
-   code: the returned status code
-   detector\_app\_version: the client version
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   release: the application version number
-   sr: the screen resolution

|-   count: the number of successful API calls
-   avg\_time: the average response time for successful API calls |
|webstat.apifailtime|Response time for failed API calls|-   api: the API request address without parameters
-   code: the returned status code
-   detector\_app\_version: the client version
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   release: the application version number
-   sr: the screen resolution

|-   count: the number of failed API calls
-   avg\_time: the average response time for failed API calls |
|webstat.apimsg|API message clustering|-   code: the returned status code
-   detector\_app\_version: the client version
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   msg: the error message
-   release: the application version number
-   sr: the screen resolution
-   success: The value 1 indicates that the request is successful and 0 indicates that the request has failed.

|count: the number of requests |
|webstat.avg|Custom statistics: average|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   key: the custom event
-   sr: the screen resolution

|-   count: the total number of occurrences of specified events
-   pv: the number of page views
-   uv: the number of unique visitors
-   avg\_val: the average value |
|webstat.errcate|Error message ranking|-   msg: the error message
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   sr: the screen resolution
-   release: the application version number
-   environment: the environment
-   detector\_app\_version: the client version
-   detector\_app: the client app

|count: the number of errors |
|webstat.index|Page view overview|-   ct: the network connection type
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_isp: the carrier
-   ip\_region\_id: the ID of a country or region outside China
-   page: the URL of the page
-   sr: the screen resolution

|-   pv: the number of page views
-   uv: the number of unique visitors |
|webstat.msg.top|Frequent errors|-   msg: the error message
-   page: the URL of the page

|-   count: the number of errors
-   error\_uv: the number of affected users
-   Ratio of affected users: the ratio obtained by dividing affected users by total UVs |
|webstat.perf.bucket|Performance Stacked Area Chart on the **Page Speed** page in the ARMS console|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   page: the URL of the page
-   sr: the screen resolution

|-   cfpt: the custom time when the first pixel is painted onto the screen
-   ctti: the custom time when a user can interact with a web page element after the page is rendered
-   dns: the time consumed for DNS query
-   dom: the time consumed for DOM resolution
-   fmp: the time when the primary content of the page becomes visible
-   fpt: the time when the first pixel is painted onto the screen
-   load: the time consumed to completely load the page
-   ready: the time consumed to load an HTML page, or the time when the DOM is ready
-   res: the time consumed to load resources
-   ssl: the time consumed to establish an SSL connection
-   t1 ~ t10: the custom performance metrics
-   tcp: the time consumed to establish a TCP connection
-   trans: the time consumed to transfer data
-   ttfb: the time consumed to respond to a network request
-   tti: the time when a user can interact with a web page element after the page is rendered |
|webstat.perf.distribution|Performance Stacked Area Chart on the **Page Speed** page in the ARMS console|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   page: the URL of the page
-   sr: the screen resolution

|-   cfpt: the custom time when the first pixel is painted onto the screen
-   ctti: the custom time when a user can interact with a web page element after the page is rendered
-   dns: the time consumed for DNS query
-   dom: the time consumed for DOM resolution
-   fmp: the time when the primary content of the page becomes visible
-   fpt: the time when the first pixel is painted onto the screen
-   load: the time consumed to completely load the page
-   ready: the time consumed to load an HTML page, or the time when the DOM is ready
-   res: the time consumed to load resources
-   ssl: the time consumed to establish an SSL connection
-   t1 ~ t10: the custom performance metrics
-   tcp: the time consumed to establish a TCP connection
-   trans: the time consumed to transfer data
-   ttfb: the time consumed to respond to a network request
-   tti: the time when a user can interact with a web page element after the page is rendered |
|webstat.resource|Resource error ranking|-   ct: the network connection type
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_isp: the carrier
-   ip\_region\_id: the ID of a country or region outside China
-   node\_name: the error type
-   page: the URL of the page
-   sr: the screen resolution
-   src: the resource information

|count: the number of resource errors|
|webstat.resource|Resource Error on the **Overview** page in the ARMS console|-   ct: the network connection type
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_isp: the carrier
-   ip\_region\_id: the ID of a country or region outside China
-   node\_name: the error type
-   page: the URL of the page
-   sr: the screen resolution
-   src: the resource information

|count: the number of resource errors|
|webstat.satisfy|Satisfaction|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   page: the URL of the page
-   sr: the screen resolution

|-   bad: frustrated, indicating that the value of fpt is greater than 8,000
-   good: satisfied, indicating that the value of fpt is smaller than 2,000
-   neutral: tolerable, indicating that the value of fpt is between 2,000 and 8,000
-   satisfy: Application Performance Index \(APDEX\) |
|webstat.session|Slow loading tracking|N/A|-   browser\_version: the browser version
-   browser: the browser
-   date: the start time of the data query
-   dom: the time consumed for DOM resolution
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_country: the province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   ip\_region: the country or region outside China
-   load: the time used to completely load the page
-   page: the URL of the page
-   sid: the session ID |
|webstat.speed|Page speed|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   release: the application version number
-   sr: the screen resolution
-   page: the URL of the page
-   environment: the environment

|-   avg\_cfpt: the average custom time when the first pixel is painted onto the screen
-   count: the number of samples
-   avg\_ctti: the average custom time when a user can interact with a web page element after the page is rendered
-   avg\_dns: the average time consumed for DNS query
-   avg\_dom: the average time consumed for DOM resolution
-   avg\_fmp: the average time when the primary content of the page becomes visible
-   avg\_fpt: the average time when the first pixel is painted onto the screen
-   avg\_load: the average time consumed to completely load the page
-   avg\_ready: the average time consumed to load an HTML page, or the average time when the DOM is ready
-   avg\_res: the average time consumed to load resources
-   avg\_ssl: the average time consumed to establish an SSL connection
-   avg\_t1~t10: the custom performance metrics
-   avg\_tcp: the average time consumed to establish a TCP connection
-   avg\_trans: the average time consumed to transfer data
-   avg\_ttfb: the average time consumed to respond to a network request
-   avg\_tti: the average time when a user can interact with a web page element after the page is rendered |
|webstat.stable|Error rate ranking|-   page: the URL of the page
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   sr: the screen resolution
-   msg: the error message
-   release: the application version number
-   environment: the environment
-   detector\_app\_version: the client version
-   detector\_app: the client app

|-   count: the number of samples
-   error\_pv: the number of JS errors
-   rate: JS error rate |
|webstat.sum|Custom statistics: sum|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   key: the custom event
-   sr: the screen resolution

|-   count: the total number of occurrences of specified events
-   pv: the number of page views
-   sum\_val: the total value
-   uv: the number of unique visitors |
|webstat.url|Access URL|-   detector\_browser: the browser
-   detector\_device: the device
-   detector\_os: the operating system
-   ip\_country\_id: the ID of a province, municipality, or autonomous region in China
-   ip\_region\_id: the ID of a country or region outside China
-   sr: the screen resolution
-   uid
-   username: the username

|-   pv: the number of page views
-   uv: the number of unique visitors |

## Examples

Sample request

```
http(s)://[Endpoint]/? Action=QueryMetricByPage
&EndTime=1596183532000
&IntervalInSec=60000
&Measures.1=pv
&Metric=webstat.index
&StartTime=1595319532000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<QueryMetricByPageResponse>
      <RequestId>626037F5-FDEB-45B0-804C-B3C92797****</RequestId>
      <Message>message</Message>
      <Data>
            <PageSize>10</PageSize>
            <Total>0</Total>
            <Page>1</Page>
            <Items>[]</Items>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</QueryMetricByPageResponse>
```

`JSON` format

```
{
    "RequestId": "626037F5-FDEB-45B0-804C-B3C92797****",
    "Message": "message",
    "Data": {
        "PageSize": 10,
        "Total": 0,
        "Page": 1,
        "Items": "[]"
    },
    "Code": 200,
    "Success": true
}
```

## FAQ

-   Why does a RAM permission error occur when I call the API?

    This is because the RAM user does not have permissions. You can grant permissions to the RAM user. For more information, see [Use a RAM role to access resources across Alibaba Cloud accounts](/intl.en-US/Access control/Use RAM roles to access resources across Alibaba cloud accounts.md).

-   How do I query a list of data entries without specifying a time interval?

    Set the intervalinsc parameter to 2147483647.

-   Why is 0 returned for all the queries?

    -   Check whether the time interval that you set is too short. Make sure that the value of the intervalinfo parameter is greater than or equal to 60,000.
    -   Check whether the value of the regionId parameter is valid. The regionId parameter is set based on the region where the server that receives logs resides, rather than the region where you reside. You can identify the region ID based on the following URLs of the log source:
        -   URL of the log source in the China \(Hangzhou\) region: `https://arms-retcode.aliyuncs.com/r.png?`
        -   URL of the log source in the Singapore region: `https://arms-retcode-sg.aliyuncs.com/r.png?`
        -   URL of the log source in the US \(Silicon Valley\) region: `https://retcode-us-west-1.arms.aliyuncs.com/r.png?`
-   Why does an error occur when I call the simulator or API?

    -   Check whether the regionId parameter is set and the value of the pid parameter is added to the filters parameter.
    -   Check whether the value of the measures or dimensions parameter of a metric is valid. For more information, see [Queryable Browser Monitoring metrics](#section_2wv_zz8_zw7).
-   Error messages and solutions

    -   **Query error. Contact the administrator.**
        -   Check whether the value of the Metric parameter is valid.
        -   Check whether the value of the measures or dimensions parameter is valid.
        -   Check whether the value of the pid parameter is added to the filters parameter.
    -   **InvalidIntervalInSec**

        Check whether the value of the intervalInSec parameter exceeds the maximum value, that is, 2147483647.

    -   **MissingMeasures**

        Check whether the measures parameter is specified.

    -   **NonsequenceParameter.Dimensions**
        -   Check whether the value of the dimensions parameter is valid.
        -   Check the simulator dimensions for extra spaces.
    -   **ServiceUnavailable**

        Check whether the value of the regionId parameter is valid.

    -   **Invalid Region**

        Check whether the value of the regionId parameter is valid. The regionId parameter is set based on the region where a server that receives logs resides, rather than the region where you reside. You can identify the region ID based on the following URLs of the log source:

        -   URL of the log source in the China \(Hangzhou\) region: `https://arms-retcode.aliyuncs.com/r.png?`
        -   URL of the log source in the Singapore region: `https://arms-retcode-sg.aliyuncs.com/r.png?`
        -   URL of the log source in the US \(Silicon Valley\) region: `https://retcode-us-west-1.arms.aliyuncs.com/r.png?`
-   Why are some parameters in the measures or dimensions parameters missing from my dataset?

    That is because you can specify a maximum of five measurement data entries or dimensions. If more than five of them are specified, no responses can be returned.

-   Why does the total number of metrics significantly decrease after they are aggregated? For example, the total number of PVs summed by webstat.index significantly decreases after the PVs are aggregated.

    A maximum of 10,000 data entries are returned due to the limit of the point of presence \(PoP\). If data is aggregated, the data volume is increased and only some data entries are returned. Therefore, the total number of metrics decreases. You must make sure that less than 10,000 data entries are returned for each request. This ensures that you can obtain accurate data.


