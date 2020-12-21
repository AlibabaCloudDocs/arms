# AddIntegration

Integrates the dashboard and collection rules of Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=AddIntegration&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddIntegration|The operation that you want to perform. Set the value to `AddIntegration`. |
|ClusterId|String|Yes|cc7a37ee31aea4ed1a059eff8034b\*\*\*\*|The ID of an Alibaba Cloud Container Service for Kubernetes cluster. |
|Integration|String|Yes|asm|The software abbreviation that is supported by ARMS. Valid values \(case-insensitive\): `ASM`, `IoT`, and `Flink`. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|success|Indicates whether the integration was successful. |
|RequestId|String|1A9C645C-C83F-4C9D-8CCB-29BEC9E1\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=AddIntegration
&ClusterId=cc7a37ee31aea4ed1a059eff8034b****
&Integration=asm
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AddIntegrationResponse>
	  <RequestId>1A9C645C-C83F-4C9D-8CCB-29BEC9E1****</RequestId>
	  <Data>success</Data>
</AddIntegrationResponse>
```

`JSON` format

```
{
    "RequestId": "1A9C645C-C83F-4C9D-8CCB-29BEC9E1****",
    "Data": "success"
}
```

