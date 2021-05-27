# SearchTraces

调用SearchTraces接口查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。

**说明：** 该接口最多返回100条数据。如需查询全量数据，建议使用SearchTracesByPage。具体详情，请参见[SearchTracesByPage](~~175866~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchTraces&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchTraces|系统规定参数，取值为`SearchTraces`。 |
|EndTime|Long|是|1595210400000|结束时间的时间戳，精确到毫秒。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|StartTime|Long|是|1595174400000|开始时间的时间戳，精确到毫秒。 |
|ServiceName|String|否|arms-k8s-demo-subcomponent|应用名称。 |
|OperationName|String|否|/demo/queryNotExistDB/11|埋点的接口名称。 |
|MinDuration|Long|否|2|最小耗时，单位为毫秒。 |
|Tag.N.Key|String|否|http.status\_code|Tag的主键。 |
|Tag.N.Value|String|否|200|Tag的值。 |
|Reverse|Boolean|否|false|按照时间正序或者倒序排列。默认值为`false`。

 -   `true`：表示倒序
-   `false`：表示正序 |
|ServiceIp|String|否|172.20.XX.XX|应用所在机器的IP地址。 |
|ExclusionFilters.N.Key|String|否|http.status\_code|用于排除的筛选条件的主键。 |
|ExclusionFilters.N.Value|String|否|404|用于排除的筛选条件的值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4C518054-852F-4023-ABC1-4AF95FF7\*\*\*\*|请求ID |
|TraceInfos|Array of TraceInfo| |返回的调用链路详细信息 |
|Duration|Long|6|调用链路耗时（毫秒） |
|OperationName|String|get\*\*\*|埋点的接口名称 |
|ServiceIp|String|172.20.\*\*.\*\*|应用所在机器的IP地址 |
|ServiceName|String|arms-k8s-demo-subcomponent|应用名称 |
|Timestamp|Long|1595174436993|时间戳 |
|TraceID|String|ac1400a115951744369937024d\*\*\*\*|调用链路ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchTraces
&EndTime=1595210400000
&RegionId=cn-hangzhou
&StartTime=1595174400000
&OperationName=/demo/queryNotExistDB/11
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

