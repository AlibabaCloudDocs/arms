# SetRetcodeShareStatus

Sets the sharing switch at the browser monitoring site.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SetRetcodeShareStatus&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetRetcodeShareStatus|The operation that you want to perform. Set the value to **SetRetcodeShareStatus**. |
|Pid|String|Yes|123123|The ID of the application. |
|Status|Boolean|Yes|true|The status of the sharing switch at the browser monitoring site. Valid values:

 -   true: The sharing switch is turned on.
-   false: The sharing switch is turned off. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the setting was successful or failed. |
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|The ID of the request. |

## Examples

Sample requests

```
http(s)://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/SetRetcodeShareStatus.json? Pid=123123&Status=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetRetcodeShareStatus>
      <IsSuccess>true</IsSuccess>
      <RequestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</RequestId>
</SetRetcodeShareStatus>
```

`JSON` format

```
{
    "IsSuccess": true,
    "RequestId": "01FF8DD9-A09C-47A1-895A-B6E321BE77B6"
}
```

