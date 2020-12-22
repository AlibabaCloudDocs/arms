# DeleteAlertContact

Deletes an DeleteAlertContact contact.

**** ****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=DeleteAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAlertContact|The parameter specified by the system. Valid values: `DeleteAlertContact` . |
|ContactId|Long|Yes|123|The ID of the alert contact to be deleted. You can call the SearchAlertContact operation to query the contact ID. For more information, see [SearchAlertContact](~~130703~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. The default is `cn-hangzhou` . |
|ProxyUserId|String|No|1234\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the contact is deleted.

 -   `true` : deleted successfully
-   `false` : deletion failed |
|RequestId|String|78901766-3806-4E96-8E47-CFEF59E4\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=DeleteAlertContact &ContactId=123 &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <DeleteAlertContactResponse> <IsSuccess>true</IsSuccess> <RequestId>78901766-3806-4E96-8E47-CFEF59E4****</RequestId> </DeleteAlertContactResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "78901766-3806-4E96-8E47-CFEF59E4****" } 
   
```

