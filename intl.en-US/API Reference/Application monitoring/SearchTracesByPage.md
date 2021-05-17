# SearchTracesByPage

Queries traces by time, application name, IP address, span name, and tag.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchTracesByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTracesByPage|The operation that you want to perform. Set the value to SearchTracesByPage. |
|EndTime|Long|Yes|1595210400000|The end of the time range to query. Unit: milliseconds. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|StartTime|Long|Yes|1595174400000|The beginning of the time range to query. Unit: milliseconds. |
|ServiceName|String|No|arms-k8s-demo-subcomponent|The name of the application. |
|OperationName|String|No|/demo/queryNotExistDB/11|The name of the span to trace. |
|MinDuration|Long|No|2|The minimum time consumed by the trace. Unit: milliseconds. |
|Reverse|Boolean|No|false|Specifies whether to sort the query results in chronological order or reverse chronological order. Default value`: false`. Valid values:

 -   `true`: Sort the query results in reverse chronological order.
-   `false`: Sort the query results in chronological order. |
|ServiceIp|String|No|172.20.XX.XX|The IP address of the host where the application resides. |
|ExclusionFilters.N.Key|String|No|http.status\_code|The key that is used to filter the query results. |
|ExclusionFilters.N.Value|String|No|404|The value of the key that is used to filter the query results. |
|PageNumber|Integer|No|1|The number of the page to return. |
|PageSize|Integer|No|5|The number of entries to return on each page. Maximum value: 100. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The struct returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|5|The number of entries returned per page. |
|Total|Integer|1601|The total number of returned entries. |
|TraceInfos|Array of TraceInfo| |The details of the returned trace. |
|Duration|Long|679|The time consumed by the trace. Unit: milliseconds. |
|OperationName|String|/demo/queryException/12|The name of the traced span. |
|ServiceIp|String|172.20.XX.XX|The IP address of the host where the application resides. |
|ServiceName|String|arms-k8s-demo-subcomponent|The name of the application. |
|Timestamp|Long|1595174436994|The timestamp when the trace was returned. |
|TraceID|String|ac1400a115951744369947025d\*\*\*\*|The ID of the trace. |
|RequestId|String|89EAC197-6636-407C-9B6E-C0478948\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchTracesByPage
&EndTime=1595210400000
&RegionId=cn-hangzhou
&StartTime=1595174400000
&PageNumber=1
&PageSize=5
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchTracesByPageResponse>
	  <PageBean>
		    <PageSize>5</PageSize>
		    <PageNumber>1</PageNumber>
		    <Total>1601</Total>
		    <TraceInfos>
			      <ServiceIp>172.20.XX.XX</ServiceIp>
			      <OperationName>/demo/queryException/12</OperationName>
			      <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
			      <TraceID>ac1400a115951744369947025d****</TraceID>
			      <Duration>2</Duration>
			      <Timestamp>1595174436994</Timestamp>
		    </TraceInfos>
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
			      <OperationName>/demo/queryUser/10</OperationName>
			      <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
			      <TraceID>ac1400a115951744969857031d****</TraceID>
			      <Duration>679</Duration>
			      <Timestamp>1595174496985</Timestamp>
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
			      <OperationName>/demo/queryException/12</OperationName>
			      <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
			      <TraceID>ac1400a115951745017577035d****</TraceID>
			      <Duration>2</Duration>
			      <Timestamp>1595174501761</Timestamp>
		    </TraceInfos>
	  </PageBean>
	  <RequestId>89EAC197-6636-407C-9B6E-C0478948****</RequestId>
</SearchTracesByPageResponse>
```

`JSON` format

```
{
	"PageBean": {
		"PageSize": 5,
		"PageNumber": 1,
		"Total": 1601,
		"TraceInfos": [
			{
				"ServiceIp": "172.20.XX.XX",
				"OperationName": "/demo/queryException/12",
				"ServiceName": "arms-k8s-demo-subcomponent",
				"TraceID": "ac1400a115951744369947025d****",
				"Duration": 2,
				"Timestamp": 1595174436994
			},
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
				"OperationName": "/demo/queryUser/10",
				"ServiceName": "arms-k8s-demo-subcomponent",
				"TraceID": "ac1400a115951744969857031d****",
				"Duration": 679,
				"Timestamp": 1595174496985
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
				"OperationName": "/demo/queryException/12",
				"ServiceName": "arms-k8s-demo-subcomponent",
				"TraceID": "ac1400a115951745017577035d****",
				"Duration": 2,
				"Timestamp": 1595174501761
			}
		]
	},
	"RequestId": "89EAC197-6636-407C-9B6E-C0478948****"
}
```

