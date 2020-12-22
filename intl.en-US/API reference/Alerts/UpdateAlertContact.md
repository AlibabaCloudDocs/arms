# UpdateAlertContact

Updates UpdateAlertContact alert contacts.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=UpdateAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateAlertContact|The parameter specified by the system. Valid values: `UpdateAlertContact` . |
|ContactId|Long|Yes|123|The ID of the alert contact to be updated. You can call the SearchAlertContact operation to query the ID. For more information, see [SearchAlertContact](~~130703~~) . |
|ContactName|String|Yes|John Doe|Change the alarm contact name to this name. |
|DingRobotWebhookUrl|String|Yes|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|Change the Webhook URL of the DingTalk robot to this value. For more information about how to obtain the URL, see [Set DingTalk robot alert](~~106247~~) . You must specify at least one of the following fields: PhoneNum, Email, and DingRobotWebhookUrl.

 **Note:** If this parameter is empty, it indicates that the parameter of the alarm contact is deleted. If this parameter is set to a value, the parameter for the alarm contact is updated. |
|Email|String|Yes|someone@example.com|Modify the email address of the alarm contact to this value. You must specify at least one of the following fields: PhoneNum, Email, and DingRobotWebhookUrl.

 **Note:** If this parameter is empty, it indicates that the parameter of the alarm contact is deleted. If this parameter is set to a value, the parameter for the alarm contact is updated. |
|PhoneNum|String|Yes|1381111\*\*\*\*|Modify the mobile phone number of the alarm contact to this value. You must specify at least one of the following fields: PhoneNum, Email, and DingRobotWebhookUrl.

 **Note:** If this parameter is empty, it indicates that the parameter of the alarm contact is deleted. If this parameter is set to a value, the parameter for the alarm contact is updated. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Always fill `cn-hangzhou` . |
|SystemNoc|Boolean|Yes|true|Indicates whether the system notifications were received. Valid values:

 -   `true` : receive system notifications
-   `false` : do not receive system notifications |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Is the update of the contact successful:

 -   true: The update succeeds.
-   false: update failed. |
|RequestId|String|1A474FF8-7861-4D00-81B5-5BC3DA4E\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=UpdateAlertContact &ContactId=123 &ContactName=John Doe &DingRobotWebhookUrl= https://oapi.dingtalk.com/robot/send?access_token=91f2f6 ******&Email=someone@example.com &PhoneNum=1381111 ******&RegionId=cn-hangzhou &SystemNoc=true &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <UpdateAlertContactResponse> <IsSuccess>true</IsSuccess> <RequestId>1A474FF8-7861-4D00-81B5-5BC3DA4E****</RequestId> </UpdateAlertContactResponse> 
   
```

`JSON`

```

     { "IsSuccess": true, "RequestId": "1A474FF8-7861-4D00-81B5-5BC3DA4E****" } 
   
```

