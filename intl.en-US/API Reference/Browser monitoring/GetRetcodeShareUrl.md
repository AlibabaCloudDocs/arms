# GetRetcodeShareUrl

Queries the sharing URL at the frontend monitoring site.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetRetcodeShareUrl&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetRetcodeShareUrl|The operation that you want to perform. Set the value to **GetRetcodeShareUrl**. |
|Pid|String|Yes|iioe7jcnuk@582846f37\*\*\*\*\*\*|The process identifier \(PID\) of the application. For more information, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|The ID of the request. |
|Url|String|http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login\_arms\_t3h\_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1|The sharing URL at the frontend monitoring site. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetRetcodeShareUrl
&Pid=iioe7jcnuk@582846f37******
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetRetcodeShareUrlResponse>
      <requestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
      <url>http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&amp;action=RetcodeAction&amp;eventSubmitDoGetData=1</url>
</GetRetcodeShareUrlResponse>
```

`JSON` format

```
{
	"requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
    "url":"http://arms-daily.console.aliyun.com:8080/shareapi/retcode.json?login_arms_t3h_token=XXXxxx&action=RetcodeAction&eventSubmitDoGetData=1"
}
```

