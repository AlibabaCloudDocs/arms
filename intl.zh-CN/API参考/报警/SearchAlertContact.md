# SearchAlertContact

调用SearchAlertContact接口查询报警联系人。

************

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertContact|系统规定参数，取值为`SearchAlertContact`。 |
|RegionId|String|是|cn-hangzhou|地域ID。始终填写`cn-hangzhou`。 |
|ContactName|String|否|John Doe|报警联系人名称。 |
|Phone|String|否|1381111\*\*\*\*\*|报警联系人电话号码。 |
|Email|String|否|someone@example.com|联系人邮箱地址。 |
|CurrentPage|String|否|1|查询分页的当前页码。 |
|PageSize|String|否|20|查询分页的每页项目数量。 |
|ContactIds|String|否|12345|报警联系人ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回结构体 |
|Contacts|Array of Contact| |联系人对象列表 |
|ContactId|Long|123|联系人ID |
|ContactName|String|John Doe|联系人名称 |
|CreateTime|Long|1572349025000|创建时间的时间戳 |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|钉钉机器人Webhook URL |
|Email|String|someone@example.com|联系人邮箱地址 |
|Phone|String|1381111\*\*\*\*\*|联系人电话号码 |
|SystemNoc|Boolean|false|是否接收系统通知：

 -   `true`：接收系统通知
-   `false`：不接收系统通知 |
|UpdateTime|Long|1580258717000|更新时间的时间戳 |
|UserId|String|113197164949\*\*\*\*|用户ID |
|Webhook|String|\{\\"body\\":\\"\{ \\\\\\"msg\_type\\\\\\": \\\\\\"text\\\\\\", \\\\\\"content\\\\\\": \{ \\\\\\"text\\\\\\": \\\\\\"$content\\\\\\" \} \}\\",\\"header\\":\{\\"Arms-Content-Type\\":\\"json\\"\},\\"method\\":\\"post\\",\\"params\\":\{\},\\"url\\":\\"https://\*\*\*",\\"userId\\":\\"1131971649\*\*\*\\"\}",|WebHook信息 |
|PageNumber|Integer|1|返回结果的页码 |
|PageSize|Integer|10|返回结果的每页项目数量 |
|TotalCount|Integer|23|返回结果的总项数数量 |
|RequestId|String|21E85B16-75A6-429A-9F65-8AAC9A54\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchAlertContact
&RegionId=cn-hangzhou
&ContactName=John Doe
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

