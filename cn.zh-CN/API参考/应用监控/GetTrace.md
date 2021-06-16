# GetTrace

调用GetTrace接口获取调用链详情。

**说明：** Java SDK需更新至版本v2.7.24。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetTrace&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTrace|系统规定参数，取值为`GetTrace`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|TraceID|String|是|ac14001a15954493811405707d\*\*\*\*|调用链ID。可在ARMS控制台的**调用链路查询**页面或**接口快照**页面获取。 |
|StartTime|Long|否|1623827602000|开始时间的时间戳，精确到毫秒。

 **说明：** 若TraceID长度为30，可不填；若TraceID长度不是30，则必填。 |
|EndTime|Long|否|1623827603000|结束时间的时间戳，精确到毫秒。

 **说明：** 若TraceID长度为30，可不填；若TraceID长度不是30，则必填。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Spans|Array of Span| |调用链路详情信息 |
|Duration|Long|1000|调用链路耗时（毫秒） |
|HaveStack|Boolean|false|是否有方法栈：

 -   `true`：有方法栈
-   `false`：没有方法栈 |
|LogEventList|Array of LogEvent| |调用链路中的日志事件 |
|TagEntryList|Array of TagEntry| |调用链路的Tag列表 |
|Key|String|http.status.code|Tag的主键 |
|Value|String|200|Tag的值 |
|Timestamp|Long|1590388651|时间戳 |
|OperationName|String|/api/demo|埋点的接口名称 |
|ParentSpanId|String|18| |
|ResultCode|String|222|返回码 |
|RpcId|String|0|RPC ID |
|RpcType|Integer|1|RPC类型 |
|ServiceIp|String|172.20.XX.XX|应用所在机器的IP地址 |
|ServiceName|String|arms-demo|应用名称 |
|SpanId|String|1234| |
|TagEntryList|Array of TagEntry| |调用链路的Tag列表 |
|Key|String|http.status.code|Tag的主键 |
|Value|String|200|Tag的值 |
|Timestamp|Long|1590388651|时间戳 |
|TraceID|String|ac14001a15954493811405707d\*\*\*\*|调用链路ID |
|RequestId|String|6A9AEA84-7186-4D8D-B498-4585C6A2\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetTrace
&RegionId=cn-hangzhou
&TraceID=ac14001a15954493811405707d****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetTraceResponse>
  <RequestId>6A9AEA84-7186-4D8D-B498-4585C6A2****</RequestId>
  <Spans>
        <HaveStack>false</HaveStack>
        <ParentSpanId>18</ParentSpanId>
        <ServiceIp>172.20.XX.XX</ServiceIp>
        <ServiceName>arms-demo</ServiceName>
        <OperationName>/api/demo</OperationName>
        <RpcType>1</RpcType>
        <RpcId>0</RpcId>
        <TraceID>ac14001a15954493811405707d****</TraceID>
        <Duration>1000</Duration>
        <Timestamp>1590388651</Timestamp>
        <ResultCode>222</ResultCode>
        <SpanId>1234</SpanId>
        <TagEntryList>
              <Value>200</Value>
              <Key>http.status.code</Key>
        </TagEntryList>
        <LogEventList>
              <Timestamp>1590388651</Timestamp>
              <TagEntryList>
                    <Value>200</Value>
                    <Key>http.status.code</Key>
              </TagEntryList>
        </LogEventList>
  </Spans>
</GetTraceResponse>
```

`JSON`格式

```
{
    "RequestId": "6A9AEA84-7186-4D8D-B498-4585C6A2****",
    "Spans": {
        "HaveStack": false,
        "ParentSpanId": 18,
        "ServiceIp": "172.20.XX.XX",
        "ServiceName": "arms-demo",
        "OperationName": "/api/demo",
        "RpcType": 1,
        "RpcId": 0,
        "TraceID": "ac14001a15954493811405707d****",
        "Duration": 1000,
        "Timestamp": 1590388651,
        "ResultCode": 222,
        "SpanId": 1234,
        "TagEntryList": {
            "Value": 200,
            "Key": "http.status.code"
        },
        "LogEventList": {
            "Timestamp": 1590388651,
            "TagEntryList": {
                "Value": 200,
                "Key": "http.status.code"
            }
        }
    }
}
```

