# DeleteAlertContactGroup

Deletes an DeleteAlertContactGroup contact group.

**** ****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=DeleteAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAlertContactGroup|The parameter specified by the system. Valid values: `DeleteAlertContactGroup` . |
|ContactGroupId|Long|Yes|123|The ID of the contact group to be deleted. You can call the SearchAlertContactGroup operation to query the ID of a group. For more information, see [SearchAlertContactGroup](~~130671~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. The default is `cn-hangzhou` . |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the alert contact group is deleted.

 -   `true` : deleted successfully
-   `false` : deletion failed |
|RequestId|String|C21AB7CF-B7AF-410F-BD61-82D1567F\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=DeleteAlertContactGroup &ContactGroupId=123 &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <DeleteAlertContactGroupResponse> <IsSuccess>true</IsSuccess> <RequestId>C21AB7CF-B7AF-410F-BD61-82D1567F****</RequestId> </DeleteAlertContactGroupResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "C21AB7CF-B7AF-410F-BD61-82D1567F****" } 
   
```

