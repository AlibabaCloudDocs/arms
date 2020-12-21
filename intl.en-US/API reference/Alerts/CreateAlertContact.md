# CreateAlertContact

You can call this operation to create an alert contact.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=CreateAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAlertContact|The operation that you want to perform. Set this value to `CreateAlertContact`. |
|ContactName|String|Yes|JohnDoe|The name of the alert contact that you want to create. |
|DingRobotWebhookUrl|String|Yes|123456|The DingTalk Chatbot address of the contact. |
|Email|String|Yes|johndoe@example.com|The email address of the contact. |
|PhoneNum|String|Yes|1381111\*\*\*\*|The phone number of the contact. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|SystemNoc|Boolean|Yes|true|Specifies whether to receive system alerts. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactId|String|6258|The ID of the alert contact that you created. |
|RequestId|String|C21AB7CF-B7AF-410F-BD61-82D1567F65F8|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/CreateAlertContact.json?ContactName=JohnDoe
&DingRobotWebhookUrl=123456
&Email=johndoe@example.com
&PhoneNum=1381111****
&RegionId=cn-hangzhou
&SystemNoc=true
&<Common request parameters>

```

Sample success response

`XML` format

```
<CreateAlertContact>
      <RequestId>C21AB7CF-B7AF-410F-BD61-82D1567F65F8</RequestId>
      <ContactId>6258</ContactId>
</CreateAlertContact>
```

`JSON` format

```
{
	"contactId":"6258",
	"requestId":"C21AB7CF-B7AF-410F-BD61-82D1567F65F8"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

