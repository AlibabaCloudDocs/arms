# ListSpanNames

调用 ListSpanNames 获取某个地域下所有的 Span 名称，也可获取某个微服务的所有 Span 名称。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=ListSpanNames&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListSpanNames|系统规定参数，取值为 `ListSpanNames`。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为 `cn-beijing` 等。 |
|ServiceName|String|否|service 1|服务名称，又称为应用名称。 |
|StartTime|Long|否|1575561600000|开始时间，精确到毫秒（ms）。 |
|EndTime|Long|否|1575622455686|结束时间，精确到毫秒（ms）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID |
|SpanNames|List|"SpanNames": \{ "SpanName": \[ "rpc0", "rpc1.1", "rpc1.1.1"\]\}|Span 名称列表 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListSpanNames
&RegionId=cn-beijing
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SpanNames>
    <SpanName>rpc0</SpanName>
    <SpanName>rpc1.1</SpanName>
    <SpanName>rpc1.1.1</SpanName>
</SpanNames>
<RequestId>79C84C64-9951-477E-96F3-7FA44128C601</RequestId>
```

`JSON` 格式

```
{
  "SpanNames": {
    "SpanName": [
      "rpc0",
      "rpc1.1",
      "rpc1.1.1"]
      },
  "RequestId": "79C84C64-9951-477E-96F3-7FA44128C601"
}
```

