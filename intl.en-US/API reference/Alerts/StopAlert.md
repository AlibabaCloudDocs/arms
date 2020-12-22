# StopAlert

Call StartAlert to stop an alert rule.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=StopAlert&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StopAlert|The operation that you want to perform. Value: StopAlert |
|AlertId|String|Yes|1610\*\*\*|The ID of the alert rule. You can call the SearchAlertRules operation to query the rule ID and set the corresponding response parameter . `Id` , please refer to [SearchAlertRules](~~175825~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Always fill `cn-hangzhou` . |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the operation is successful. Valid values:

 -   `true` : Operation succeeded
-   `false` : Operation failed |
|RequestId|String|27E653FA-5958-45BE-8AA9-14D884DC\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=StopAlert &AlertId=1610 stopprobe * &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <StopAlertResponse> <IsSuccess>true</IsSuccess> <RequestId>27E653FA-5958-45BE-8AA9-14D884DC****</RequestId> </StopAlertResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "27E653FA-5958-45BE-8AA9-14D884DC****" } 
   
```

