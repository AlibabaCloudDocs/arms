# SetRetcodeShareStatus

Turns on or off the logon-free sharing switch for an application monitored by the frontend monitoring feature.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SetRetcodeShareStatus&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetRetcodeShareStatus|The operation that you want to perform. Set the value to `SetRetcodeShareStatus`. |
|Pid|String|Yes|atc889zkcf@d8deedfa9bf\*\*\*\*|The process identifier \(PID\) of the application. For more information, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |
|Status|Boolean|Yes|true|Specifies whether to turn on or turn off the logon-free sharing switch. Valid values:

 -   `true`: Turn on the switch.
-   `false`: Turn off the switch. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the call is successful. Valid values:

 -   `true`: The call is successful.
-   `false`: The call fails. |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SetRetcodeShareStatus
&Pid=atc889zkcf@d8deedfa9bf****
&Status=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetRetcodeShareStatusResponse>
      <IsSuccess>true</IsSuccess>
      <RequestId>40B10E04-81E8-4643-970D-F1B38F2E****</RequestId>
</SetRetcodeShareStatusResponse>
```

`JSON` format

```
{
    "IsSuccess": true,
    "RequestId": "40B10E04-81E8-4643-970D-F1B38F2E****"
}
```

