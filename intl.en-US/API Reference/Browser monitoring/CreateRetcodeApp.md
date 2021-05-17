# CreateRetcodeApp

Creates a frontend monitoring task for an application.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=CreateRetcodeApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateRetcodeApp|The operation that you want to perform. Set the value to CreateRetcodeApp. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|Yes|SdkTest|The name of the application to be monitored by the frontend monitoring feature. |
|RetcodeAppType|String|Yes|mini\_dd|The type of the application to be monitored by the frontend monitoring feature. Valid values: `web`, `weex`, `mini_dd`, `mini_alipay`, `mini_wx`, and `mini_common`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|The ID of the request. |
|RetcodeAppDataBean|Struct| |The information about the frontend monitoring task. |
|AppId|Long|135143|The ID of the application. |
|Pid|String|aokcdqn3ly@a195c6d6421\*\*\*\*|The process identifier \(PID\) of the application. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CreateRetcodeApp
&RegionId=cn-hangzhou
&RetcodeAppName=SdkTest
&RetcodeAppType=mini_dd
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateRetcodeAppResponse>
      <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C647A</RequestId>
      <RetcodeAppDataBean>
            <AppId>135143</AppId>
            <Pid>aokcdqn3ly@a195c6d6421****</Pid>
      </RetcodeAppDataBean>
</CreateRetcodeAppResponse>
```

`JSON` format

```
{
    "RequestId": "A5EC8221-08F2-4C95-9AF1-49FD998C647A",
    "RetcodeAppDataBean": {
        "AppId": 135143,
        "Pid": "aokcdqn3ly@a195c6d6421****"
    }
}
```

