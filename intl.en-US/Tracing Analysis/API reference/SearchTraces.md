# SearchTraces

Queries all traces. You can filter traces by time, service name, IP address, span name, and tag.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=SearchTraces&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraces|The operation that you want to perform. Set the value to `SearchTraces`. |
|EndTime|Long|Yes|1575622455686|The end of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|StartTime|Long|Yes|1575561600000|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |
|ServiceName|String|No|service 1|The name of the microservice. |
|OperationName|String|No|/api|The name of a span. |
|MinDuration|Long|No|1000|The minimum time of period used to collect traced data. Unit: milliseconds. For example, the value 100 indicates that you can filter the returned entries with a time period no less than 100 milliseconds on collecting traced data. |
|AppType|String|No|XTRACE|The type of the service. This parameter is optional. You can set the value to `XTRACE`. |
|Tag.N.Key|String|No|http.status\_cod|The key of the tag. |
|Tag.N.Value|String|No|200|The value of the tag. |
|PageNumber|Integer|No|1|The number of the page to return. For example, the value 5 indicates page 5. |
|PageSize|Integer|No|100|The number of entries to return on each page. |
|Reverse|Boolean|No|false|The method of sorting the returned entries. For example, the value true indicates the reverse chronological order. The value false indicates the chronological order. Default value: false. |
|ServiceIp|String|No|10.0.0.0|The IP address of the server in which the span resides. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The information of the returned page. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|100|The number of entries returned per page. |
|TotalCount|Long|1000|The total number of entries. |
|TraceInfos|Array| |The information of the trace. |
|TraceInfo| | | |
|Duration|Long|100|The time used to call a trace. Unit: microseconds. |
|OperationName|String|/api|The name of the span. |
|ServiceIp|String|192.163.0.1|The IP address of the server in which the span resides. |
|ServiceName|String|service1|The name of the microservice. |
|Timestamp|Long|1575561600000000|The time when the span was generated. Unit: microseconds. |
|TraceID|String|1c6881aab84191a4|The ID of the trace. |
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchTraces
&EndTime=1575622455686
&RegionId=cn-beijing
&StartTime=1575561600000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<PageBean>
    <TotalCount>17539818</TotalCount>
    <PageSize>10</PageSize>
    <TraceInfos>
        <TraceInfo>
            <ServiceIp>11.194.110.238</ServiceIp>
            <OperationName>checkAndRefresh</OperationName>
            <ServiceName>xtrace-collector</ServiceName>
            <TraceID>547713e07af0139e</TraceID>
            <Duration>0</Duration>
            <Timestamp>1583683202048</Timestamp>
        </TraceInfo>
    </TraceInfos>
</PageBean>
<RequestId>B00B2E34-416A-46D7-8894-05EAD557947A</RequestId>
```

`JSON` format

```
{
  "PageBean": {
    "TotalCount": 17539818,
    "PageSize": 10,
    "TraceInfos": {
      "TraceInfo": [
        {
          "ServiceIp": "11.194.110.238",
          "OperationName": "checkAndRefresh",
          "ServiceName": "xtrace-collector",
          "TraceID": "547713e07af0139e",
          "Duration": 0,
          "Timestamp": 1583683202048
        }]
        }
        },
        "RequestId": "B00B2E34-416A-46D7-8894-05EAD557947A"
        }
```

