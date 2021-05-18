# CreateAlertContact

Creates an alert contact.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=CreateAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAlertContact|The operation that you want to perform. Set the value to CreateAlertContact. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Set the value to `cn-hangzhou`. |
|ContactName|String|No|JohnDoe|The name of the alert contact. |
|PhoneNum|String|No|1381111\*\*\*\*|The mobile number of the alert contact. You must specify at least one of the following parameters: PhoneNum, Email, and DingRobotWebhookUrl. |
|Email|String|No|someone@example.com|The email address of the alert contact. You must specify at least one of the following parameters: PhoneNum, Email, and DingRobotWebhookUrl. |
|DingRobotWebhookUrl|String|No|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|The webhook URL of the DingTalk chatbot. For more information about how to obtain the URL, see [Configure a DingTalk chatbot to send alert notifications](https://www.alibabacloud.com/help/zh/doc-detail/106247.htm). You must specify at least one of the following parameters: PhoneNum, Email, and DingRobotWebhookUrl.

 **Note:** Enter `alert` in the custom keyword field of DingTalk chatbot security settings. |
|SystemNoc|Boolean|No|true|Specifies whether the alert contact receives system notifications. Valid values:

 -   `true`: receives system notifications.
-   `false`: does not receive system notifications. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactId|String|102\*\*|The ID of the alert contact. |
|RequestId|String|E9C9DA3D-10FE-472E-9EEF-2D0A3E41\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CreateAlertContact
&ContactName=JohnDoe
&DingRobotWebhookUrl=https://oapi.dingtalk.com/robot/send?access_token=91f2f6****
&Email=someone@example.com
&PhoneNum=1381111****
&RegionId=cn-hangzhou
&SystemNoc=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAlertContactResponse>
	  <RequestId>E9C9DA3D-10FE-472E-9EEF-2D0A3E41****</RequestId>
	  <ContactId>102**</ContactId>
</CreateAlertContactResponse>
```

`JSON` format

```
{
    "RequestId": "E9C9DA3D-10FE-472E-9EEF-2D0A3E41****",
    "ContactId": "102**"
}
```

