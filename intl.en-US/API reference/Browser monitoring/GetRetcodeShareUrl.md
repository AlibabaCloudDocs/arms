# GetRetcodeShareUrl

Queries the sharing URL at the browser monitoring site.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetRetcodeShareUrl&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetRetcodeShareUrl|The operation that you want to perform. Set the value to **GetRetcodeShareUrl**. |
|Pid|String|Yes|123123|The ID of the application. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|The ID of the request. |
|Url|String|http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login\_arms\_t3h\_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1|The sharing URL at the browser monitoring site. |

## Examples

Sample requests

```
http(s)://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/GetRetcodeShareUrl.json? Pid=123123
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetRetcodeShareUrl>
    <requestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
    <url>http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1</url>
</GetRetcodeShareUrl>
```

`JSON` format

```
{
	"requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
    "url":"http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1"
}
```

