# GetTrace

Queries the information of a trace.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=GetTrace&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTrace|The operation that you want to perform. Set the value to `GetTrace`. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|TraceID|String|Yes|1c6881aab84191a4|The ID of the trace. It is the unique identifier of the trace. |
|AppType|String|No|XTRACE|The type of the service. The parameter is optional. You can set the value to `XTRACE`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. If an error is returned, you can submit a ticket. The error is located based on the RequestId. |
|Spans|Array| |The information of the trace. |
|Span| | | |
|Duration|Long|1000|The time used to call a trace. Unit: microseconds. For example, the value 1000 indicates 1 millisecond. |
|HaveStack|Boolean|false|Indicates whether the span has child spans. |
|LogEventList|Array| |The log events in the trace. |
|LogEvent| | | |
|TagEntryList|Array| |The list of tags. |
|TagEntry| | | |
|Key|String|logLevel|The tag key in the log events. |
|Value|String|Warning|The value in the log events. |
|Timestamp|Long|1583683202047000|The time when the log event was generated. |
|OperationName|String|/api|The name of a span. |
|ResultCode|String|200|The status code. |
|RpcId|String|1.1|The parent-child and sibling relationship between spans. For example, span 1.1 is the parent of span 1.1.1, and span 1.1.2 and span 1.1.1 are siblings. |
|ServiceIp|String|192.168.0.1|The IP address of the server in which the span resides. |
|ServiceName|String|server1|The name of the microservice in which the trace resides. |
|TagEntryList|Array| |The list of tags in the span. |
|TagEntry| | | |
|Key|String|logLevel|The key of the tag. |
|Value|String|Warning|The value of the tag. |
|Timestamp|Long|1583683202047000|The time when the span was generated. |
|TraceID|String|1c6881aab84191a4|The ID of the trace. It is the unique identifier of the trace. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetTrace
&RegionId=cn-beijing
&TraceID=1c6881aab84191a4
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

