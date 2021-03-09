# GetTagKey

调用 GetTagKey 获取上报链路数据中的 Tag Key。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=GetTagKey&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTagKey|系统规定参数，取值为 `GetTagKey`。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为 `cn-beijing` 等。 |
|ServiceName|String|否|appTest|应用名称，即上报数据中填写的微服务名称。 |
|SpanName|String|否|createOrder|Span 埋点时设置的名称，又称为 OperationName。 |
|StartTime|Long|否|1575561600000|开始时间，精确到毫秒（ms）。 |
|EndTime|Long|否|1575622455686|结束时间，精确到毫秒（ms）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID |
|TagKeys|List|"TagKeys": \{ "TagKey": \[ "error.kind","span.kind"\]\}|返回的 Tag Key 列表 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetTagKey
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<TagKeys>
    <TagKey>date</TagKey>
    <TagKey>resultCount</TagKey>
    <TagKey>aTid</TagKey>
    <TagKey>dbName</TagKey>
    <TagKey>pid</TagKey>
    <TagKey>conf</TagKey>
    <TagKey>error</TagKey>
    <TagKey>type</TagKey>
    <TagKey>getSt</TagKey>
    <TagKey>eventSubmitDoGetConfig</TagKey>
    <TagKey>measures</TagKey>
    <TagKey>eventSubmitDoSelectTopoInfo</TagKey>
    <TagKey>span.kind</TagKey>
    <TagKey>eventSubmitDoGetDatas</TagKey>
    <TagKey>action</TagKey>
    <TagKey>startTime</TagKey>
    <TagKey>sn</TagKey>
    <TagKey>stageId</TagKey>
    <TagKey>st</TagKey>
    <TagKey>sampler.type</TagKey>
    <TagKey>k1</TagKey>
    <TagKey>IsCompleted</TagKey>
    <TagKey>sampler.param</TagKey>
    <TagKey>grpc.status</TagKey>
    <TagKey>param3</TagKey>
    <TagKey>userId</TagKey>
    <TagKey>param1</TagKey>
    <TagKey>param2</TagKey>
    <TagKey>reqId</TagKey>
    <TagKey>http.status_code</TagKey>
    <TagKey>component</TagKey>
    <TagKey>IntervalInSecond</TagKey>
    <TagKey>error.kind</TagKey>
    <TagKey>regionId</TagKey>
    <TagKey>metric</TagKey>
    <TagKey>lb</TagKey>
    <TagKey>eventSubmitDoGetRpcTypeInfoList</TagKey>
    <TagKey>_metric</TagKey>
    <TagKey>intervalMillis</TagKey>
    <TagKey>endTime</TagKey>
    <TagKey>bid</TagKey>
    <TagKey>did</TagKey>
    <TagKey>getEt</TagKey>
    <TagKey>db</TagKey>
    <TagKey>dimensions</TagKey>
</TagKeys>
<RequestId>7D6519C1-A92A-4F07-AC83-706D48204242</RequestId>
```

`JSON` 格式

```
{
	"TagKeys": {
		"TagKey": [
			"date",
			"resultCount",
			"aTid",
			"dbName",
			"pid",
			"conf",
			"error",
			"type",
			"getSt",
			"eventSubmitDoGetConfig",
			"measures",
			"eventSubmitDoSelectTopoInfo",
			"span.kind",
			"eventSubmitDoGetDatas",
			"action",
			"startTime",
			"sn",
			"stageId",
			"st",
			"sampler.type",
			"k1",
			"IsCompleted",
			"sampler.param",
			"grpc.status",
			"param3",
			"userId",
			"param1",
			"param2",
			"reqId",
			"http.status_code",
			"component",
			"IntervalInSecond",
			"error.kind",
			"regionId",
			"metric",
			"lb",
			"eventSubmitDoGetRpcTypeInfoList",
			"_metric",
			"intervalMillis",
			"endTime",
			"bid",
			"did",
			"getEt",
			"db",
			"dimensions"
		]
	},
	"RequestId": "7D6519C1-A92A-4F07-AC83-706D48204242"
}
```

