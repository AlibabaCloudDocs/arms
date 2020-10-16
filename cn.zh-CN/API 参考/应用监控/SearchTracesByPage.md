# SearchTracesByPage

调用SearchTracesByPage接口分页查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchTracesByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EndTime|Long|是|1595210400000|结束时间的时间戳，精确到毫秒。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|StartTime|Long|是|1595174400000|开始时间的时间戳，精确到毫秒。 |
|ServiceName|String|否|arms-k8s-demo-subcomponent|应用名称。 |
|OperationName|String|否|/demo/queryNotExistDB/11|埋点的接口名称。 |
|MinDuration|Long|否|2|最小耗时，单位为毫秒。 |
|Reverse|Boolean|否|false|按照时间正序或者倒序排列。默认值为`false`。

 -   `true`：表示倒序
-   `false`：表示正序 |
|ServiceIp|String|否|172.20.XX.XX|应用所在机器的IP地址。 |
|ExclusionFilters.N.Key|String|否|http.status\_code|用于排除的筛选条件的主键。 |
|ExclusionFilters.N.Value|String|否|404|用于排除的筛选条件的值。 |
|PageNumber|Integer|否|1|查询分页的页码。 |
|PageSize|Integer|否|5|查询分页的每页项目数量，最大值为100。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回结构体 |
|PageNumber|Integer|1|返回结果的页码 |
|PageSize|Integer|5|返回结果的每页项目数量 |
|Total|Integer|1601|返回结果的总项目数量 |
|TraceInfos|Array of TraceInfo| |返回的调用链路详细信息 |
|Duration|Long|679|调用链路耗时（毫秒） |
|OperationName|String|/demo/queryException/12|埋点的接口名称 |
|ServiceIp|String|172.20.XX.XX|应用所在机器的IP地址 |
|ServiceName|String|arms-k8s-demo-subcomponent|应用名称 |
|Timestamp|Long|1595174436994|时间戳 |
|TraceID|String|ac1400a115951744369947025d\*\*\*\*|调用链路ID |
|RequestId|String|89EAC197-6636-407C-9B6E-C0478948\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchTracesByPage
&EndTime=1595210400000
&RegionId=cn-hangzhou
&StartTime=1595174400000
&PageNumber=1
&PageSize=5
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

