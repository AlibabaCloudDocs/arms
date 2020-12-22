# GetTrace

Queries detailed information of a trace.

**** **** ****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=GetTrace&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTrace|The parameter specified by the system. Valid values: `GetTrace` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceID|String|Yes|ac14001a15954493811405707d\*\*\*\*|The ID of the trace. You can view the **trace** in the ARMS console Page or **interface snapshot** Obtain page. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Spans|Array| |The returned details about the trace. |
|Duration|Long|1000|The time consumed by the trace. Unit: millisecond. |
|HaveStack|Boolean|false|Is there a method stack:

 -   `true` : method stack
-   `false` : no method stack |
|LogEventList|Array| |The log events in the trace. |
|TagEntryList|Array| |The tag list in the trace. |
|Key|String|http.status.code|The primary key of the tag. |
|Value|String|200|The value of the tag. |
|Timestamp|Long|1590388651|The timestamp when the trace was returned. |
|OperationName|String|/api/demo|The name of the traced span. |
|ResultCode|String|222|The returned code. |
|RpcId|String|0|RPC ID |
|RpcType|Integer|1|The type of Remote Procedure Call \(RPC\). |
|ServiceIp|String|172.20.XX.XX|The IP address of the host where the application resides. |
|ServiceName|String|arms-demo|Application |
|TagEntryList|Array| |The tag list in the trace. |
|Key|String|http.status.code|The primary key of the tag. |
|Value|String|200|The value of the tag. |
|Timestamp|Long|1590388651|The timestamp when the trace was returned. |
|TraceID|String|ac14001a15954493811405707d\*\*\*\*|The ID of the trace. |
|RequestId|String|6A9AEA84-7186-4D8D-B498-4585C6A2\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=GetTrace &RegionId=cn-hangzhou &TraceID=ac14001a15954493811405707d *** &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <GetTraceResponse> <RequestId>6A9AEA84-7186-4D8D-B498-4585C6A2****</RequestId> <Spans> <HaveStack>true</HaveStack> <ServiceIp>172.20.XX.XX</ServiceIp> <OperationName>/api/demo</OperationName> <ServiceName>arms-demo</ServiceName> <RpcId>0.1</RpcId> <RpcType>0</RpcType> <TraceID>ac14001a15954493811405707d****</TraceID> <Duration>1000</Duration> <TagEntryList> <Value>200</Value> <Key>http.status.code</Key> </TagEntryList> <TagEntryList> <Value>172.20.XX.XX</Value> <Key>source.ip</Key> </TagEntryList> <Timestamp>1590388651</Timestamp> <ResultCode>0</ResultCode> </Spans> </GetTraceResponse> 
   
```

`JSON`

```

     { "RequestId": "6A9AEA84-7186-4D8D-B498-4585C6A2****", "Spans": [ { "HaveStack": true, "ServiceIp": "172.20.XX.XX", "LogEventList": [], "OperationName": "/api/demo", "ServiceName": "arms-demo", "RpcId": "0.1", "RpcType": 0, "TraceID": "ac14001a15954493811405707d****", "Duration": 1000, "TagEntryList": [ { "Value": "200", "Key": "http.status.code" }, { "Value": "172.20.XX.XX", "Key": "source.ip" } ], "Timestamp": 1590388651, "ResultCode": "0" } ] } 
   
```

