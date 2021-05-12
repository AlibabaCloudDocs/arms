# GetAppApiByPage

调用GetAppApiByPage接口分页查询前端应用接口数据。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetAppApiByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAppApiByPage|系统规定参数。取值：`GetAppApiByPage`。 |
|EndTime|Long|是|1600066800000|结束时间的时间戳，精确到毫秒。 |
|PId|String|是|xxx@74xxx|应用的唯一识别码。`pid`获取方式请参见[如何获取前端应用PID](https://www.alibabacloud.com/help/zh/doc-detail/183682.htm?spm=a2c63.l28256.b99.342.252412727XCKUD#h2-url-3)。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|StartTime|Long|是|1600063200000|开始时间的时间戳，精确到毫秒。 |
|CurrentPage|Integer|否|1|查询结果的页码。 |
|PageSize|Integer|否|10|查询结果的每页项目数量。 |
|IntervalMills|Integer|否|60000|数据片的时间间隔，单位为毫秒，最小值为60000。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|Integer|200|接口状态。取值：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结构体。 |
|Items|List|\[\]|返回应用接口数据的详细信息。 |
|Page|Integer|1|返回结果的页码。 |
|PageSize|Integer|10|返回结果的每页项目数量。 |
|Total|String|0|返回结果的总项目数量。 |
|Message|String|message|返回结果的提示信息。 |
|RequestId|String|B6A00968-82A8-4F14-9D1B-B53827DB\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询是否成功。取值：

 -   `true`：成功。
-   `false`：失败。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetAppApiByPage
&EndTime=1600066800000
&PId=xxx@74xxx
&RegionId=cn-hangzhou
&StartTime=1600063200000
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetAppApiByPageResponse>
	  <RequestId>B6A00968-82A8-4F14-9D1B-B53827DB****</RequestId>
	  <Message>message</Message>
	  <Data>
		    <PageSize>10</PageSize>
		    <Total>0</Total>
		    <Page>1</Page>
		    <Items>[]</Items>
	  </Data>
	  <Code>200</Code>
	  <Success>true</Success>
</GetAppApiByPageResponse>
```

`JSON`格式

```
{
    "RequestId": "B6A00968-82A8-4F14-9D1B-B53827DB****",
    "Message": "message",
    "Data": {
        "PageSize": 10,
        "Total": 0,
        "Page": 1,
        "Items": "[]"
    },
    "Code": 200,
    "Success": true
}
```

