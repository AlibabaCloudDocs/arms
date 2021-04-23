# DeletePrometheusAlertRule

Deletes an alert rule of Prometheus Service.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DeletePrometheusAlertRule&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeletePrometheusAlertRule|The operation that you want to perform. Set the value to DeletePrometheusAlertRule. |
|AlertId|Long|Yes|3888704|The ID of the alert rule. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the request is successful. Valid values:

 -   `true`: The alert rule was deleted.
-   `false`: The request failed. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DeletePrometheusAlertRule
&AlertId=3888704
&<Common Request Parameters>
```

Sample success responses

`XML` format

```
<DeletePrometheusAlertRuleResponse>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
  <Success>true</Success>
</DeletePrometheusAlertRuleResponse>
```

`JSON` format

```
{
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****",
    "Success": true
}
```

