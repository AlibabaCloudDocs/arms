# GetTagVal

调用 GetTagVal 获取上报的链路数据中指定 Tag Key 对应的 Tag Value。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=GetTagVal&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTagVal|系统规定参数，取值为 `GetTagVal`。 |
|TagKey|String|是|span.kind|用于上报的链路数据中的 Tag Key。 |
|RegionId|String|否|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为 `cn-beijing` 等。 |
|ServiceName|String|否|appTest|应用名称，即上报数据中填写的微服务名称。 |
|SpanName|String|否|createOrder|Span 埋点时设置的名称，又称为 Operation Name。 |
|StartTime|Long|否|1575561600000|开始时间，精确到毫秒（ms）。 |
|EndTime|Long|否|1575622455686|结束时间，精确到毫秒（ms）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID |
|TagValues|List|"TagValues": \{ "TagValue": \[ "server" \] \}|返回的 Tag Value 列表 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetTagVal
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>D36507D4-FD30-430B-BEC4-738661CFB86C</RequestId>
<TagValues>
    <TagValue>server</TagValue>
</TagValues>
```

`JSON` 格式

```
{
	"RequestId": "D36507D4-FD30-430B-BEC4-738661CFB86C",
	"TagValues": {
		"TagValue": [
			"server"
		]
	}
}
```

