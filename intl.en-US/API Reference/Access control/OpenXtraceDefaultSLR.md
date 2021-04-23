# OpenXtraceDefaultSLR

Activates the service-linked role AliyunServiceRoleForXtrace for Tracing Analysis.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=OpenXtraceDefaultSLR&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|OpenXtraceDefaultSLR|The operation that you want to perform. Set the value to OpenXtraceDefaultSLR. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|true|Indicates whether the call was successful. Valid values:

 -   `true`: successful
-   `false`: failed |
|RequestId|String|53CACA70-2CF7-490C-BD06-1A2AE4EB\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=OpenXtraceDefaultSLR
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<OpenXtraceDefaultSLRResponse>
  <RequestId>53CACA70-2CF7-490C-BD06-1A2AE4EB****</RequestId>
  <Data>true</Data>
</OpenXtraceDefaultSLRResponse>
```

`JSON` format

```
{
    "RequestId": "53CACA70-2CF7-490C-BD06-1A2AE4EB****",
    "Data": true
}
```

