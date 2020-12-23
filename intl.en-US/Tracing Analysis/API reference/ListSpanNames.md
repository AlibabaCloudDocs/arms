# ListSpanNames

Queries the names of all spans in a region or microservice.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=ListSpanNames&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListSpanNames|The operation that you want to perform. Set the value to `ListSpanNames`. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|ServiceName|String|No|service 1|The name of the service. |
|StartTime|Long|No|1575561600000|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |
|EndTime|Long|No|1575622455686|The end of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |
|SpanNames|List|"SpanNames": \{ "SpanName": \[ "rpc0", "rpc1.1", "rpc1.1.1"\]\}|The list of span names. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListSpanNames
&RegionId=cn-beijing
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SpanNames>
    <SpanName>rpc0</SpanName>
    <SpanName>rpc1.1</SpanName>
    <SpanName>rpc1.1.1</SpanName>
</SpanNames>
<RequestId>79C84C64-9951-477E-96F3-7FA44128C601</RequestId>
```

`JSON` format

```
{
  "SpanNames": {
    "SpanName": [
      "rpc0",
      "rpc1.1",
      "rpc1.1.1"]
      },
  "RequestId": "79C84C64-9951-477E-96F3-7FA44128C601"
}
```

