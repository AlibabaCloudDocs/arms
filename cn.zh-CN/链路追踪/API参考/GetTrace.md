# GetTrace

调用 GetTrace 获取调用链路详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=GetTrace&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTrace|系统规定参数，取值为 `GetTrace`。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为`cn-beijing` 等。 |
|TraceID|String|是|1c6881aab84191a4|调用链 ID，链路请求的唯一标识。 |
|AppType|String|否|XTRACE|应用类型，非必选项，可填写为 `XTRACE` 或不填。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID。上报出现异常时，可添加工单并根据 RequestId 查询失败原因。 |
|Spans|Array| |链路详情信息。 |
|Span| | | |
|Duration|Long|1000|耗时，单位是微秒。例如 1000 表示 1 毫秒。 |
|HaveStack|Boolean|false|是否有 Child Span。 |
|LogEventList|Array| |链路数据中的 Log Event。 |
|LogEvent| | | |
|TagEntryList|Array| |返回的 Tag 列表。 |
|TagEntry| | | |
|Key|String|logLevel|Log Event 中的 Tag Key。 |
|Value|String|Warning|Log Event 中的 Value。 |
|Timestamp|Long|1583683202047000|Log Event 的产生时间。 |
|OperationName|String|/api|某个埋点名称，又称为 Span Name。 |
|ResultCode|String|200|返回码。 |
|RpcId|String|1.1|表示 Span 之间的父子兄弟关系。 例如 1.1 是 1.1.1 的父亲 Span， 而 1.1.2 和 1.1.1 是兄弟 Span。 |
|ServiceIp|String|192.168.0.1|Span 所在的机器 IP 地址。 |
|ServiceName|String|server1|链路所在的微服务名称，又称为应用名称。 |
|TagEntryList|Array| |Span 中的 Tag 列表。 |
|TagEntry| | | |
|Key|String|logLevel|Tag Key。 |
|Value|String|Warning|Tag Value。 |
|Timestamp|Long|1583683202047000|Span 的产生时间。 |
|TraceID|String|1c6881aab84191a4|调用链 ID，链路请求的唯一标识。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetTrace
&RegionId=cn-beijing
&TraceID=1c6881aab84191a4
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>0C1E24B7-A83B-4CFE-AC19-72193092F2E7</RequestId>
<Spans>
    <Span>
        <HaveStack>false</HaveStack>
        <ServiceIp>11.194.110.238</ServiceIp>
        <LogEventList>
        </LogEventList>
        <OperationName>/adapt_b31oxdxruh@1e6391553ea2619_b31oxdxruh@53df7ad2afe8301/api/traces</OperationName>
        <ServiceName>xtrace-collector</ServiceName>
        <RpcId>1</RpcId>
        <TraceID>547713e07af0139e</TraceID>
        <Duration>341</Duration>
        <TagEntryList>
            <TagEntry>
                <Value>0</Value>
                <Key>st</Key>
            </TagEntry>
            <TagEntry>
                <Value>200</Value>
                <Key>http.status_code</Key>
            </TagEntry>
            <TagEntry>
                <Value>server</Value>
                <Key>span.kind</Key>
            </TagEntry>
        </TagEntryList>
        <Timestamp>1583683202047000</Timestamp>
        <ResultCode>0</ResultCode>
    </Span>
</Spans>
```

`JSON` 格式

```
{
  "RequestId": "0C1E24B7-A83B-4CFE-AC19-72193092F2E7",
  "Spans": {
    "Span": [
      {
        "HaveStack": false,
        "ServiceIp": "11.194.110.238",
        "LogEventList": {
          "LogEvent": []
        },
        "OperationName": "/api/traces",
        "ServiceName": "xtrace-collector",
        "RpcId": "1",
        "TraceID": "547713e07af0139e",
        "Duration": 341,
        "TagEntryList": {
          "TagEntry": [
            {
              "Value": "0",
              "Key": "st"
            },
            {
              "Value": "200",
              "Key": "http.status_code"
            },
            {
              "Value": "server",
              "Key": "span.kind"
            }
          ]
        },
        "Timestamp": "1583683202047000",
        "ResultCode": "0"
      }]
    }
    }
```

