# GetPrometheusApiToken

Queries the token required for integrating Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetPrometheusApiToken&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetPrometheusApiToken|The operation that you want to perform. Set the value to `GetPrometheusApiToken`. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1A9C645C-C83F-4C9D-8CCB-29BEC9E1\*\*\*\*|The ID of the request. |
|Token|String|6dcbb77ef4ba6ef5466b5debf9e2\*\*\*\*|The token required for integrating ARMS Prometheus Monitoring. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetPrometheusApiToken
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetPrometheusApiTokenResponse>
	  <RequestId>1A9C645C-C83F-4C9D-8CCB-29BEC9E1****</RequestId>
	  <Token>6dcbb77ef4ba6ef5466b5debf9e2****</Token>
</GetPrometheusApiTokenResponse>
```

`JSON` format

```
{
    "RequestId": "1A9C645C-C83F-4C9D-8CCB-29BEC9E1****",
    "Token": "6dcbb77ef4ba6ef5466b5debf9e2****"
}
```

