# SearchAlertContact

Queries alert contacts.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertContact|The operation that you want to perform. Set the value to `SearchAlertContact`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Set the value to `cn-hangzhou`. |
|ContactName|String|No|John Doe|The name of the alert contact. |
|Phone|String|No|1381111\*\*\*\*\*|The mobile number of the alert contact. |
|Email|String|No|someone@example.com|The email address of the alert contact. |
|CurrentPage|String|No|1|The number of the page to return. |
|PageSize|String|No|20|The number of entries to return on each page. |
|ContactIds|String|No|12345|The ID of the alert contact. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The struct returned. |
|Contacts|Array of Contact| |The information about the alert contacts. |
|ContactId|Long|123|The ID of the alert contact. |
|ContactName|String|John Doe|The name of the alert contact. |
|CreateTime|Long|1572349025000|The timestamp when the alert contact was created. |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|The webhook URL of the DingTalk chatbot. |
|Email|String|someone@example.com|The email address of the alert contact. |
|Phone|String|1381111\*\*\*\*\*|The mobile number of the alert contact. |
|SystemNoc|Boolean|false|Indicates whether the alert contact receives system notifications. Valid values:

-   `true`: receives system notifications.
-   `false`: does not receive system notifications. |
|UpdateTime|Long|1580258717000|The timestamp when the alert contact was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|Webhook|String|\{\\"body\\":\\"\{ \\\\\\"msg\_type\\\\\\": \\\\\\"text\\\\\\", \\\\\\"content\\\\\\": \{ \\\\\\"text\\\\\\": \\\\\\"$content\\\\\\" \} \}\\",\\"header\\":\{\\"Arms-Content-Type\\":\\"json\\"\},\\"method\\":\\"post\\",\\"params\\":\{\},\\"url\\":\\"https://\*\*\*",\\"userId\\":\\"1131971649\*\*\*\\"\}",|The information about the webhook. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|23|The total number of returned entries. |
|RequestId|String|21E85B16-75A6-429A-9F65-8AAC9A54\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchAlertContact
&RegionId=cn-hangzhou
&ContactName=John Doe
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertContactResponse>
  <PageBean>
        <TotalCount>23</TotalCount>
        <PageSize>10</PageSize>
        <Contacts>
              <Email>someone@example.com</Email>
              <UserId>113197164949****</UserId>
              <Phone>1381111*****</Phone>
              <CreateTime>1572349025000</CreateTime>
              <UpdateTime>1580258717000</UpdateTime>
              <Webhook>{\"body\":\"{   \\\"msg_type\\\": \\\"text\\\",   \\\"content\\\": {     \\\"text\\\": \\\"$content\\\"   } }\",\"header\":{\"Arms-Content-Type\":\"json\"},\"method\":\"post\",\"params\":{},\"url\":\"https://***",\"userId\":\"1131971649***\"}",</Webhook>
              <ContactId>123</ContactId>
              <DingRobot>https://oapi.dingtalk.com/robot/send?access_token=91f2f6****</DingRobot>
              <SystemNoc>false</SystemNoc>
              <ContactName>John Doe</ContactName>
        </Contacts>
        <PageNumber>1</PageNumber>
  </PageBean>
  <RequestId>21E85B16-75A6-429A-9F65-8AAC9A54****</RequestId>
</SearchAlertContactResponse>
```

`JSON` format

```
{
    "PageBean": {
        "TotalCount": 23,
        "PageSize": 10,
        "Contacts": {
            "Email": "someone@example.com",
            "UserId": "113197164949****",
            "Phone": "1381111*****",
            "CreateTime": 1572349025000,
            "UpdateTime": 1580258717000,
            "Webhook": "{\\\"body\\\":\\\"{   \\\\\\\"msg_type\\\\\\\": \\\\\\\"text\\\\\\\",   \\\\\\\"content\\\\\\\": {     \\\\\\\"text\\\\\\\": \\\\\\\"$content\\\\\\\"   } }\\\",\\\"header\\\":{\\\"Arms-Content-Type\\\":\\\"json\\\"},\\\"method\\\":\\\"post\\\",\\\"params\\\":{},\\\"url\\\":\\\"https://***\",\\\"userId\\\":\\\"1131971649***\\\"}\",",
            "ContactId": 123,
            "DingRobot": "https://oapi.dingtalk.com/robot/send?access_token=91f2f6****",
            "SystemNoc": false,
            "ContactName": "John Doe"
        },
        "PageNumber": 1
    },
    "RequestId": "21E85B16-75A6-429A-9F65-8AAC9A54****"
}
```

