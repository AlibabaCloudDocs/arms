# SetRetcodeShareStatus

Turns on or off the logon-free sharing switch for an application monitored by Browser Monitoring.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SetRetcodeShareStatus&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetRetcodeShareStatus|The operation that you want to perform. Set the value to `SetRetcodeShareStatus`. |
|Pid|String|Yes|123123|The ID of the application. |
|Status|Boolean|Yes|true|Specifies whether to turn on or turn off the logon-free sharing switch. Valid values:

 -   `true`: on
-   `false`: off |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the call was successful.

 -   `true`: The call was successful.
-   `false`: The call failed. |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SetRetcodeShareStatus
&Pid=123123
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

