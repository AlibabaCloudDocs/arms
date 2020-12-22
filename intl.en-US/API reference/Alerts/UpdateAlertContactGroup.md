# UpdateAlertContactGroup

Updates UpdateAlertContactGroup alarm contact group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=UpdateAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateAlertContactGroup|The parameter specified by the system. Valid values: `UpdateAlertContactGroup` . |
|ContactGroupId|Long|Yes|123|The ID of the contact group to be updated. You can call the SearchAlertContactGroup operation to query the ID of a group. For more information, see [SearchAlertContactGroup](~~130671~~) . |
|ContactGroupName|String|Yes|TestGroup|Modify the name of the alarm contact group to this value. |
|ContactIds|String|Yes|12\* 23\* 34\*|The ID of the contact to include in the alarm contact group. Separate multiple contact IDs with spaces. You can call the SearchAlertContact operation to query the contact ID. For more information, see [SearchAlertContact](~~130703~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. The default is `cn-hangzhou` . |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the contact group is updated.

 -   `true` : update successful
-   `false` : update failed |
|RequestId|String|9319A57D-2D9E-472A-B69B-CF3CD16D\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=UpdateAlertContactGroup &ContactGroupId=123 &ContactGroupName=TestGroup &ContactIds=12* 23* 34 * &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <UpdateAlertContactGroupResponse> <IsSuccess>true</IsSuccess> <RequestId>9319A57D-2D9E-472A-B69B-CF3CD16D****</RequestId> </UpdateAlertContactGroupResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "9319A57D-2D9E-472A-B69B-CF3CD16D****" } 
   
```

