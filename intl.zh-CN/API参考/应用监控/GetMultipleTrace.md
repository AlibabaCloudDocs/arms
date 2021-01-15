# GetMultipleTrace

调用GetMultipleTrace接口获取多个调用链的详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetMultipleTrace&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMultipleTrace|系统规定参数，取值为`GetMultipleTrace`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|TraceIDs.N|RepeatList|是|ac1400a115951745017447033d\*\*\*\*|调用链ID，必填参数。可在[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)的调用链路查询页面或接口快照页面获取。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|MultiCallChainInfos|Array of MultiCallChainInfo| |多个调用链路的信息 |
|Spans|Array of Span| |调用链路详情信息 |
|Duration|Long|11|调用链路耗时（毫秒） |
|HaveStack|Boolean|true|是否有方法栈：

 -   `true`：有方法栈
-   `false`：没有方法栈 |
|LogEventList|Array of LogEvent| |调用链路中的日志事件 |
|TagEntryList|Array of TagEntry| |调用链路的Tag列表 |
|Key|String|http.status.code|Tag的主键 |
|Value|String|200|Tag的值 |
|Timestamp|Long|1595174501747|时间戳 |
|OperationName|String|/demo/queryNotExistDB/11|埋点的接口名称 |
|ResultCode|String|1|返回码 |
|RpcId|String|0.1|RPC ID |
|RpcType|Integer|0|RPC类型

 -   0：HTTP入口
-   25：调用HTTP
-   1：调用HSF
-   2：提供HSF
-   40：调用本地API
-   60：调用MYSQL
-   62：调用ORACLE
-   63：调用POSTGRESQL
-   70：调用REDIS
-   4：调用TDDL
-   5：调用TAIR
-   13：发送METAQ
-   252：接收METAQ
-   3：发送NOTIFY
-   254：接收NOTIFY
-   7：调用DUBBO
-   8：提供DUBBO
-   19：调用SOFA
-   18：提供SOFA
-   11：调用DSF
-   12：提供DSF
-   -1：未知调用 |
|ServiceIp|String|172.20.XX.XX|应用所在机器的IP地址 |
|ServiceName|String|arms-k8s-demo-subcomponent|应用名称 |
|TagEntryList|Array of TagEntry| |调用链路的Tag列表 |
|Key|String|http.status.code|Tag的主键 |
|Value|String|200|Tag的值 |
|Timestamp|Long|1595174501747|时间 |
|TraceID|String|ac1400a115951745017447033d\*\*\*\*|调用链路ID |
|TraceID|String|ac1400a115951745017447033d\*\*\*\*|调用链路ID |
|RequestId|String|2983BEF7-4A0D-47A2-94A2-8E9C5E63\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetMultipleTrace
&RegionId=cn-hangzhou
&TraceIDs.1=ac1400a115951745017447033d****
&TraceIDs.2=ac1400a115951745017577035d****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetMultipleTraceResponse>
	  <RequestId>2983BEF7-4A0D-47A2-94A2-8E9C5E63****</RequestId>
	  <MultiCallChainInfos>
		    <TraceID>ac1400a115951745017447033d****</TraceID>
		    <Spans>
			      <HaveStack>true</HaveStack>
			      <ServiceIp>172.20.XX.XX</ServiceIp>
			      <OperationName>/demo/queryNotExistDB/11</OperationName>
			      <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
			      <RpcId>0.1</RpcId>
			      <RpcType>0</RpcType>
			      <TraceID>ac1400a115951745017447033d****</TraceID>
			      <Duration>11</Duration>
			      <TagEntryList>
				        <Value>200</Value>
				        <Key>http.status.code</Key>
			      </TagEntryList>
			      <TagEntryList>
				        <Value>172.20.XX.XX</Value>
				        <Key>source.ip</Key>
			      </TagEntryList>
			      <Timestamp>1595174501747</Timestamp>
			      <ResultCode>1</ResultCode>
		    </Spans>
	  </MultiCallChainInfos>
	  <MultiCallChainInfos>
		    <TraceID>ac1400a115951745017577035d****</TraceID>
		    <Spans>
			      <HaveStack>true</HaveStack>
			      <ServiceIp>172.20.XX.XX</ServiceIp>
			      <OperationName>/demo/queryException/12</OperationName>
			      <ServiceName>arms-k8s-demo-subcomponent</ServiceName>
			      <RpcId>0.1</RpcId>
			      <RpcType>0</RpcType>
			      <TraceID>ac1400a115951745017577035d****</TraceID>
			      <Duration>2</Duration>
			      <TagEntryList>
				        <Value>500</Value>
				        <Key>http.status.code</Key>
			      </TagEntryList>
			      <TagEntryList>
				        <Value>172.20.XX.XX</Value>
				        <Key>source.ip</Key>
			      </TagEntryList>
			      <Timestamp>1595174501761</Timestamp>
			      <ResultCode>1</ResultCode>
		    </Spans>
	  </MultiCallChainInfos>
</GetMultipleTraceResponse>
```

`JSON` 格式

```
{
	"RequestId": "2983BEF7-4A0D-47A2-94A2-8E9C5E63****",
	"MultiCallChainInfos": [
		{
			"TraceID": "ac1400a115951745017447033d****",
			"Spans": [
				{
					"HaveStack": true,
					"ServiceIp": "172.20.XX.XX",
					"LogEventList": [],
					"OperationName": "/demo/queryNotExistDB/11",
					"ServiceName": "arms-k8s-demo-subcomponent",
					"RpcId": "0.1",
					"RpcType": 0,
					"TraceID": "ac1400a115951745017447033d****",
					"Duration": 11,
					"TagEntryList": [
						{
							"Value": "200",
							"Key": "http.status.code"
						},
						{
							"Value": "172.20.XX.XX",
							"Key": "source.ip"
						}
					],
					"Timestamp": 1595174501747,
					"ResultCode": "1"
				}
			]
		},
		{
			"TraceID": "ac1400a115951745017577035d****",
			"Spans": [
				{
					"HaveStack": true,
					"ServiceIp": "172.20.XX.XX",
					"LogEventList": [],
					"OperationName": "/demo/queryException/12",
					"ServiceName": "arms-k8s-demo-subcomponent",
					"RpcId": "0.1",
					"RpcType": 0,
					"TraceID": "ac1400a115951745017577035d****",
					"Duration": 2,
					"TagEntryList": [
						{
							"Value": "500",
							"Key": "http.status.code"
						},
						{
							"Value": "172.20.XX.XX",
							"Key": "source.ip"
						}
					],
					"Timestamp": 1595174501761,
					"ResultCode": "1"
				}
			]
		}
	]
}
```

