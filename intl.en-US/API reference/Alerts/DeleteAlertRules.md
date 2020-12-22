# DeleteAlertRules

Call the DeleteAlertRules API to delete alarm rules.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=DeleteAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAlertRules|The parameter specified by the system. Valid values: `DeleteAlertRules` . |
|AlertIds|String|Yes|\[123, 234\]|The ID list of the alarm rules that you want to delete. JSON Array, for example : `[123, 234]` . You can call the SearchAlertRules API to obtain the alarm rule ID \(corresponding to the response parameter `Id` \), please refer to [SearchAlertRules](~~175825~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. The default is `cn-hangzhou` . |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the alert rule is deleted.

 -   `true` : deleted successfully
-   `false` : deletion failed |
|RequestId|String|C21AB7CF-B7AF-410F-BD61-82D1567F\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=DeleteAlertRules &AlertIds=[123, 234] &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <DeleteAlertRulesResponse> <IsSuccess>true</IsSuccess> <RequestId>C21AB7CF-B7AF-410F-BD61-82D1567F****</RequestId> </DeleteAlertRulesResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "C21AB7CF-B7AF-410F-BD61-82D1567F****" } 
   
```

