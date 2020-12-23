# ListIpOrHosts

Queries IP addresses or host names in traced data.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=ListIpOrHosts&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListIpOrHosts|The operation that you want to perform. Set the value to `ListIpOrHosts`. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|ServiceName|String|No|service1|The name of the service. The parameter is optional. If you specify a service name, the IP addresses in this service are returned. |
|StartTime|Long|No|1583683200000|The beginning of the time range to query. |
|EndTime|Long|No|1583723776974|The end of the time range to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IpNames|List|\[ "10.0.0.0", "10.0.0.1" \]|The list of IP addresses. |
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListIpOrHosts
&RegionId=cn-beijing
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>23D9757C-CB58-41A5-BBE7-2A9A0652B2F4</RequestId>
<IpNames>
    <IpName>172.19.33.172</IpName>
    <IpName>null</IpName>
    <IpName>10.0.0.5</IpName>
</IpNames>
```

`JSON` format

```
{
  "RequestId": "23D9757C-CB58-41A5-BBE7-2A9A0652B2F4",
  "IpNames": {
    "IpName": [
      "172.19.33.172",
      "10.0.0.5"
    ]
  }
}
```

