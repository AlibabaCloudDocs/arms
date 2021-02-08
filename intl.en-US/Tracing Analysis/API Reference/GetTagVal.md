# GetTagVal

Queries the tag values that correspond to a tag key in traced data.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=GetTagVal&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTagVal|The operation that you want to perform. Set the value to `GetTagVal`. |
|TagKey|String|Yes|span.kind|The tag key in traced data. |
|RegionId|String|No|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|ServiceName|String|No|appTest|The name of the service. |
|SpanName|String|No|createOrder|The name of a span. |
|StartTime|Long|No|1575561600000|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |
|EndTime|Long|No|1575622455686|The end of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |
|TagValues|List|"TagValues": \{ "TagValue": \[ "server" \] \}|The list of tag values. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetTagVal
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>D36507D4-FD30-430B-BEC4-738661CFB86C</RequestId>
<TagValues>
    <TagValue>server</TagValue>
</TagValues>
```

`JSON` format

```
{
    "RequestId": "D36507D4-FD30-430B-BEC4-738661CFB86C",
    "TagValues": {
        "TagValue": [
            "server"
        ]
    }
}
```

