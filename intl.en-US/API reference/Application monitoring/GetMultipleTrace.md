# GetMultipleTrace

Queries the detailed information about multiple traces.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetMultipleTrace&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetMultipleTrace|The operation that you want to perform. Set the value to `GetMultipleTrace`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceIDs.N|RepeatList|No|ac1400a115951745017447033d\*\*\*\*|Required. The ID of the trace. You can log on to the ARMS console and obtain the ID on the Call Chain Query or Interface Snapshot tab. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MultiCallChainInfos|Array| |The information about multiple traces. |
|Spans|Array| |The information about the trace. |
|Duration|Long|11|The time that is consumed by the trace. Unit: milliseconds. |
|HaveStack|Boolean|true|Indicates whether a method stack was provided.

 -   `true`: The method stack exists.
-   `false` : No method stack exists. |
|LogEventList|Array| |The log events in the trace. |
|TagEntryList|Array| |The tag list in the trace. |
|Key|String|http.status.code|The primary key of the tag. |
|Value|String|200|The value of the tag. |
|Timestamp|Long|1595174501747|The timestamp. |
|OperationName|String|/demo/queryNotExistDB/11|The name of the traced span. |
|ResultCode|String|1|The response code. |
|RpcId|String|0.1|RPC ID |
|RpcType|Integer|0|The type of the remote procedure call \(RPC\). |
|ServiceIp|String|172.20.XX.XX|The IP address of the host where the application resides. |
|ServiceName|String|arms-k8s-demo-subcomponent|The name of the application. |
|TagEntryList|Array| |The tag list in the trace. |
|Key|String|http.status.code|The primary key of the tag. |
|Value|String|200|The value of the tag. |
|Timestamp|Long|1595174501747|The time |
|TraceID|String|ac1400a115951745017447033d\*\*\*\*|The ID of the trace. |
|TraceID|String|ac1400a115951745017447033d\*\*\*\*|The ID of the trace. |
|RequestId|String|2983BEF7-4A0D-47A2-94A2-8E9C5E63\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetMultipleTrace
&RegionId=cn-hangzhou
&TraceIDs.1=ac1400a115951745017447033d****
&TraceIDs.2=ac1400a115951745017577035d****
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

