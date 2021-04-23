# GetAgentDownloadUrl

Obtains the download URL of the Application Real-Time Monitoring Service \(ARMS\) agent.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetAgentDownloadUrl&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAgentDownloadUrl|The operation that you want to perform. Set the value to GetAgentDownloadUrl. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ArmsAgentDownloadUrl|String|http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/|The download URL of the ARMS agent. |
|RequestId|String|14043452-D486-4EA1-80C9-BA73FB81\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetAgentDownloadUrl
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetAgentDownloadUrlResponse>
  <ArmsAgentDownloadUrl>http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/</ArmsAgentDownloadUrl>
  <RequestId>14043452-D486-4EA1-80C9-BA73FB81****</RequestId>
</GetAgentDownloadUrlResponse>
```

`JSON` format

```
{
    "ArmsAgentDownloadUrl": "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/",
    "RequestId": "14043452-D486-4EA1-80C9-BA73FB81****"
}
```

