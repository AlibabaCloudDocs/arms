# SearchTraces

Queries all traces by time, service name, IP address, span name, and tag.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchTraces&type=RPC&version=2019-08-08)

## Request Parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraces|The operation that you want to perform. Set the value to `SearchTraces`. |
|EndTime|Long|Yes|1595210400000|The end of the time range to query.Unit: milliseconds. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |
|StartTime|Long|Yes|1595174400000|The beginning of the time range to query. Unit: milliseconds. |
|ServiceName|String|No|arms-k8s-demo-subcomponent|The name of the application. |
|OperationName|String|No|/demo/queryNotExistDB/11|The interface name of the tracking. |
|MinDuration|Long|No|2|The minimum time consumed. Unit: milliseconds. |
|Tag.N.Key|String|No|http.status\_code|The primary key of the tag. |
|Tag.N.Value|String|No|200|The value of the tag. |
|Reverse|Boolean|No|false|Specifies whether to sort the query results in chronological order or reverse chronological order. Default value`: false`.

-   `true`: indicates the reverse chronological order.
-   `false`: indicates the chronological order. |
|ServiceIp|String|No|172.20.XX.XX|The IP address of the host where the application is located. |
|ExclusionFilters.N.Key|String|No|http.status\_code|The primary key of the exclusion filter. |
|ExclusionFilters.N.Value|String|No|404|The value of the exclusion filter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4C518054-852F-4023-ABC1-4AF95FF7\*\*\*\*|The ID of the request. |
|TraceInfos|Array| |The details about the returned trace. |
|Duration|Long|6|The time consumed by a trace. Unit: millisecond. |
|OperationName|String|get\*\*\*|The interface name of the tracking. |
|ServiceIp|String|172.20.\*\*. \*\*|The IP address of the host where the application is located. |
|ServiceName|String|arms-k8s-demo-subcomponent|The name of the application. |
|Timestamp|Long|1595174436993|The timestamp. |
|TraceID|String|ac1400a115951744369937024d\*\*\*\*|The trace ID. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchTraces
&EndTime=1595210400000
&RegionId=cn-hangzhou
&StartTime=1595174400000
&OperationName=/demo/queryNotExistDB/11
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchTracesResponse>
      <RequestId>4C518054-852F-4023-ABC1-4AF95FF7****</RequestId>
      <TraceInfos>
            <ServiceIp>172.20.XX.XX</ServiceIp>
            <OperationName>/demo/queryNotExistDB/11</OperationName>
            <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
            <TraceID>ac1400a115951744369937024d****</TraceID>
            <Duration>6</Duration>
            <Timestamp>1595174436993</Timestamp>
      </TraceInfos>
      <TraceInfos>
            <ServiceIp>172.20.XX.XX</ServiceIp>
            <OperationName>/demo/queryNotExistDB/11</OperationName>
            <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
            <TraceID>ac1400a115951745017447033d****</TraceID>
            <Duration>11</Duration>
            <Timestamp>1595174501747</Timestamp>
      </TraceInfos>
      <TraceInfos>
            <ServiceIp>172.20.XX.XX</ServiceIp>
            <OperationName>/demo/queryNotExistDB/11</OperationName>
            <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
            <TraceID>ac1400a115951803817467721d****</TraceID>
            <Duration>3</Duration>
            <Timestamp>1595180381751</Timestamp>
      </TraceInfos>
</SearchTracesResponse>
```

`JSON` format

```
{
    "RequestId": "4C518054-852F-4023-ABC1-4AF95FF7****",
    "TraceInfos": [
        {
            "ServiceIp": "172.20.XX.XX",
            "OperationName": "/demo/queryNotExistDB/11",
            "ServiceName": "arms-k8s-demo-subcomponent",
            "TraceID": "ac1400a115951744369937024d****",
            "Duration": 6,
            "Timestamp": 1595174436993
        },
        {
            "ServiceIp": "172.20.XX.XX",
            "OperationName": "/demo/queryNotExistDB/11",
            "ServiceName": "arms-k8s-demo-subcomponent",
            "TraceID": "ac1400a115951745017447033d****",
            "Duration": 11,
            "Timestamp": 1595174501747
        },
        {
            "ServiceIp": "172.20.XX.XX",
            "OperationName": "/demo/queryNotExistDB/11",
            "ServiceName": "arms-k8s-demo-subcomponent",
            "TraceID": "ac1400a115951803817467721d****",
            "Duration": 3,
            "Timestamp": 1595180381751
        }
    ]
}
```

