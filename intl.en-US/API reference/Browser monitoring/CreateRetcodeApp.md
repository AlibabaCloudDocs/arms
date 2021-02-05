# CreateRetcodeApp

Creates a browser monitoring job for an application.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=CreateRetcodeApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|Yes|SdkTest|The name of the application. |
|RetcodeAppType|String|Yes|web|The type of the application that can be monitored by Browser Monitoring. Valid values: web, weex, mini\_dd, mini\_alipay, mini\_wx, and mini\_common. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|The ID of the request. |
|RetcodeAppDataBean|Struct| |The returned creation information of the browser monitoring job. |
|AppId|Long|135143|The ID of the application. |
|Pid|String|aokcdqn3ly@a195c6d6421\*\*\*\*|The PID. |

## Examples

Sample requests

```
http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/CreateRetcodeApp.json?RegionId=cn-hangzhou
&RetcodeAppName=SdkTest
&RetcodeAppType=web
```

Sample success responses

`XML` format

```
<CreateRetcodeApp>
       <requestId>A5EC8221-08F2-4C95-9AF1-49FD998C647A</requestId>
       <retcodeAppDataBean>
              <appId>135143</appId>
              <pid>aokcdqn3ly@a195c6d6421****</pid>
       </retcodeAppDataBean>
</CreateRetcodeApp>
```

`JSON` format

```
{
    "requestId": "A5EC8221-08F2-4C95-9AF1-49FD998C647A",
    "retcodeAppDataBean": {
        "appId": 135143,
        "pid": "aokcdqn3ly@a195c6d6421****"
    }
}
```

