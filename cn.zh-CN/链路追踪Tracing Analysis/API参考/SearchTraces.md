# SearchTraces

调用 SearchTraces 查询调用链列表，可根据时间、应用名称、IP 地址、Span 名称和 Tag 等信息对调用链进行过滤查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=SearchTraces&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchTraces|系统规定参数，取值为 `SearchTraces`。 |
|EndTime|Long|是|1575622455686|结束时间，精确到毫秒（ms）。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为 `cn-beijing` 等。 |
|StartTime|Long|是|1575561600000|开始时间，精确到毫秒（ms）。 |
|ServiceName|String|否|service 1|微服务名称，又称为应用名称。 |
|OperationName|String|否|/api|Span 名称，即某个跟踪点或埋点的名称。 |
|MinDuration|Long|否|1000|大于某个时间跨度范围，单位为毫秒。例如 100 表示大于 100 毫秒的数据。 |
|AppType|String|否|XTRACE|应用类型，非必选值，可填写为 `XTRACE`或不填。 |
|Tag.N.Key|String|否|http.status\_cod|Tag Key。 |
|Tag.N.Value|String|否|200|Tag Value。 |
|PageNumber|Integer|否|1|页码，例如 5 表示第 5 页。 |
|PageSize|Integer|否|100|每页的查询数据条数。 |
|Reverse|Boolean|否|false|按照时间正序或者倒序排列，true 表示倒序，false 表示顺序。默认为 false。 |
|ServiceIp|String|否|10.0.0.0|Span 对应的 IP 地址。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回数据的位置信息。 |
|PageNumber|Integer|1|页码。 |
|PageSize|Integer|100|每页显示的数据条数。 |
|TotalCount|Long|1000|总条数。 |
|TraceInfos|Array| |返回的调用链信息。 |
|TraceInfo| | | |
|Duration|Long|100|耗时，单位为毫秒（ms）。 |
|OperationName|String|/api|Span 名称。 |
|ServiceIp|String|192.163.0.1|Span 所在的 IP 地址。 |
|ServiceName|String|service1|微服务名称，又称为应用名称。 |
|Timestamp|Long|1575561600000000|Span 产生时间，单位是微秒。 |
|TraceID|String|1c6881aab84191a4|调用链 ID。 |
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchTraces
&EndTime=1575622455686
&RegionId=cn-beijing
&StartTime=1575561600000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PageBean>
    <TotalCount>17539818</TotalCount>
    <PageSize>10</PageSize>
    <TraceInfos>
        <TraceInfo>
            <ServiceIp>11.194.110.238</ServiceIp>
            <OperationName>checkAndRefresh</OperationName>
            <ServiceName>xtrace-collector</ServiceName>
            <TraceID>547713e07af0139e</TraceID>
            <Duration>0</Duration>
            <Timestamp>1583683202048</Timestamp>
        </TraceInfo>
    </TraceInfos>
</PageBean>
<RequestId>B00B2E34-416A-46D7-8894-05EAD557947A</RequestId>
```

`JSON` 格式

```
{
  "PageBean": {
    "TotalCount": 17539818,
    "PageSize": 10,
    "TraceInfos": {
      "TraceInfo": [
        {
          "ServiceIp": "11.194.110.238",
          "OperationName": "checkAndRefresh",
          "ServiceName": "xtrace-collector",
          "TraceID": "547713e07af0139e",
          "Duration": 0,
          "Timestamp": 1583683202048
        }]
        }
        },
        "RequestId": "B00B2E34-416A-46D7-8894-05EAD557947A"
        }
```

