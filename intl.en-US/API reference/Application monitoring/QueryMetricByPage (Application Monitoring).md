# QueryMetricByPage \(Application Monitoring\)

Queries the metrics of Application Monitoring.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=QueryMetricByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|QueryMetricByPage|The operation that you want to perform. Set the value to `QueryMetricByPage`. |
|EndTime|Long|Yes|1596183532000|The end of the time range to query. Unit: milliseconds. |
|IntervalInSec|Integer|Yes|60000|The time interval between the data shards to be queried. Unit: milliseconds. Minimum value: 60,000. |
|Measures.N|RepeatList|Yes|pv|The measurement data of the metric. For more information, see [Queryable Application Monitoring metrics](#section_tq8_ysr_srb). You can add a maximum of five measurement data entries.|
|Metric|String|Yes|webstat.index|The metrics that you want to query. You cannot query custom metrics. For more information, see [Queryable Application Monitoring metrics](#section_tq8_ysr_srb).|
|StartTime|Long|Yes|1595319532000|The beginning of the time range to query. Unit: milliseconds. |
|OrderBy|String|No|rpc|The measurement data entry by which metrics are sorted. You can set this parameter to a type of measurement data. |
|Filters.N.Key|String|Yes|pid|The filtering condition for the query. The `pid` and `regionId` parameters are required. For information about how to obtain the `pid`, see [Obtain the PID of an application](#section_bkl_3j6_ezg).|
|Filters.N.Value|String|Yes|xxx@74xxx|The filtering condition for the query. The `pid` and `regionId` parameters are required. For information about how to obtain the `pid`, see [Obtain the PID of an application](#section_bkl_3j6_ezg).|
|Dimensions.N|RepeatList|No|\["detector\_browser","detector\_device"\]|The dimension by which metrics are queried. For more information, see [Queryable Application Monitoring metrics](#section_tq8_ysr_srb). You can add a maximum of five measurement data entries.|
|Order|String|No|ASC|The measurement data entry by which metrics are sorted. Valid values:

-   `ASC`: ascending order
-   `DESC`: descending order |
|RegionId|String|No|cn-hangzhou|The ID of the region. |
|CurrentPage|Integer|No|1|The number of the page to return. Optional. Default value: `1`. |
|PageSize|Integer|No|10|The number of entries to return on each page. |

## Obtain the PID of an application

Log on to the [Application Real-Time Monitoring Service console](https://arms-intl.console.aliyun.com/#/home).In the top navigation bar, select a region. In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the **Browser Monitoring**page, click the name of the application that you want to query to open the overview page of this application.

The URL in the browser address bar contains the pid of this application in the format of `pid=xxx`. The browser is encoded. Therefore, you must modify the pid of all applications except for those in Enterprise Distributed Application Service \(EDAS\). For example, if the PID in the URL is `xxx%4074xxx`, you must replace `%40` with `@`. The PID is modified to `xxx@74xxx`.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|String|200|The status of the API. Valid values:

-   2XX: success
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

## Queryable Application Monitoring metrics

You can call the QueryMetricByPage operation to query the following metrics of Application Monitoring.

**Note:**

-   You must specify `pid` and `regionId` in Filters.
-   If you have obtained the values of the PID and regionId parameters, add the values to the filters parameter to define the range of query results. If you have not obtained the values of the PID and regionId parameters, pass the dimensions in the following table to the dimensions parameter to obtain a list of all possible values.

|Metric|Description|Dimension|Measurement data|
|------|-----------|---------|----------------|
|appstat.vm|Common metrics that are shown on the JVM monitoring chart of the application details page. These metrics include garbage collection \(GC\), heap memory, non-heap memory, and number of threads.|-   pid
-   rootIp

|GC: -   youngGcCount // The number of monitored young GCs in the Java virtual machine \(JVM\)
-   oldGcCount // The number of monitored full GCs in the JVM
-   youngGcTime // The time consumed to monitor young GCs in the JVM
-   oldGcTime // The time consumed to monitor full GCs in the JVM
-   youngGcCountInstant // The instantaneous value of the number of monitored young GCs in the JVM
-   oldGcCountInstant // The instantaneous value of the number of monitored full GCs in the JVM
-   youngGcTimeInstant // The instantaneous value of the time consumed to monitor young GCs in the JVM
-   oldGcTimeInstant // The instantaneous value of the time consumed to monitor full GCs in the JVM |
|Details of the heap memory and non-heap memory:-   EdenSpace // The young generation - Eden space
-   OldGen // The old generation
-   survivorSpace // The young generation - Survivor space
-   metaSpace
-   nonHeapCommitted // The non-heap memory
-   nonHeapInit // The initial value of the non-heap memory
-   nonHeapMax // The maximum value of the non-heap memory
-   nonHeapUsed // The usage of the non-heap memory
-   directUsed // The direct buffer
-   directCapacity // The direct buffer |
|Number of threads: -   threadCount
-   threadNewCount
-   threadDeadlockCount
-   threadRunnableCount
-   threadTerminatedCount
-   threadTimedWaitCount
-   threadWaitCount
-   threadBlockedCount |
|appstat.host|Host monitoring metrics. These metrics include the number of instances, CPU, physical memory, disk, load, network traffic \(in bytes\), and number of network packets.|-   pid
-   rootIp

|Number of instances: -   instanceCount |
|CPU: -   systemCpuIdle // Not displayed on the page - CPU idle
-   systemCpuSystem
-   systemCpuUser
-   systemCpuIoWait |
|Physical memory: -   systemMemFree
-   systemMemUsed
-   SystemMemTotal // Not displayed on the page - total system memory
-   systemMemBuffers
-   SystemMemCached // The page cache |
|Disk: -   systemDiskFree
-   systemDiskUsed
-   SystemDiskTotal // Not displayed in the Alibaba Cloud console - total system disk space |
|Load: -   systemLoad |
|Network: -   systemNetInPackets
-   systemNetOutPackets
-   systemNetInErrs
-   systemNetOutErrs
-   systemNetInBytes
-   systemNetOutBytes |
|appstat.database|Database call|-   pid
-   rpcType // The call type
-   endpoint // The database address: `localhost: 3306`
-   destId // The database name: `arms`

|-   rt // The response time
-   count // The number of requests
-   error // The number of errors |
|appstat.txn|API call.|-   pid
-   rpcType
-   rpc // The interface: `/demo/oracleTwo`

|-   rt
-   count
-   error
-   errRate // The error rate |
|appstat.incall|Application details|-   pid
-   rpcType
-   rootIp
-   rpc
-   ppid

|-   rt
-   count
-   error |
|appstat.exception|Exception|-   pid
-   rpc
-   endpoint
-   excepType
-   excepInfo

|-   rt
-   count |
|appstat.sql|Slow SQLs|-   pid
-   rpc
-   endpoint
-   sqlId

|-   rt
-   count
-   error
-   slow

**Note:** If you set slow to true, the limit parameter does not take effect. |
|appstat.mq.send|Message Queue \(MQ\) message sending|N/A|-   rt
-   count
-   error |
|appstat.mq.receive|MQ message receiving|N/A|-   rt
-   count
-   error |

## Examples

Sample requests

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

