# GetRetcodeShareUrl

使用GetRetcodeShareUrl获取前端监控站点的分享地址。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetRetcodeShareUrl&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetRetcodeShareUrl|系统规定参数，取值：**GetRetcodeShareUrl**。 |
|Pid|String|是|iioe7jcnuk@582846f37\*\*\*\*\*\*|应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|请求ID。 |
|Url|String|http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login\_arms\_t3h\_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1|前端监控站点的分享地址。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetRetcodeShareUrl
&Pid=iioe7jcnuk@582846f37******
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetRetcodeShareUrlResponse>
      <requestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
      <url>http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&amp;action=RetcodeAction&amp;eventSubmitDoGetData=1</url>
</GetRetcodeShareUrlResponse>
```

`JSON`格式

```
{
	"requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
    "url":"http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1"
}
```

