# SearchAlertContactGroup

调用SearchAlertContactGroup接口查询报警联系人分组。

************

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertContactGroup&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertContactGroup|系统规定参数，取值为`SearchAlertContactGroup`。 |
|RegionId|String|是|cn-hangzhou|地域ID。默认为`cn-hangzhou`。 |
|ContactGroupName|String|否|TestGroup|报警联系人分组名称。 |
|ContactName|String|否|John Doe|报警联系人名称。 |
|ContactId|Long|否|123|报警联系人ID。可调用SearchAlertContact接口来查询联系人ID，请参见[SearchAlertContact](~~130703~~)。 |
|ContactGroupIds|String|否|746|报警联系人分组ID。可以同时查询多个联系人分组ID，联系人分组ID之间用英文逗号（,）分隔。 |
|IsDetail|Boolean|否|true|是否返回联系人分组中包含的所有联系人。默认不返回所有联系人。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ContactGroups|Array of ContactGroup| |报警联系人分组信息 |
|ContactGroupId|Long|746|报警联系人分组ID |
|ContactGroupName|String|TestGroup|报警联系人分组名称 |
|Contacts|Array of Contact| |联系人对象列表 |
|ContactId|Long|123|联系人ID |
|ContactName|String|John Doe|联系人名称 |
|CreateTime|Long|1572349025000|创建时间的时间戳 |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|钉钉机器人Webhook URL |
|Email|String|someone@example.com|联系人邮箱地址 |
|Phone|String|1381111\*\*\*\*\*|联系人电话号码 |
|SystemNoc|Boolean|false|是否接收系统通知：

 -   true：接收系统通知
-   false：不接收系统通知 |
|UpdateTime|Long|1580258717000|更新时间的时间戳 |
|UserId|String|113197164949\*\*\*\*|用户ID |
|CreateTime|Long|1529668855000|创建时间的时间戳 |
|UpdateTime|Long|1529668855000|更新时间的时间戳 |
|UserId|String|113197164949\*\*\*\*|用户ID |
|RequestId|String|4D6C358A-A58B-4F4B-94CE-F5AAF023\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchAlertContactGroup
&RegionId=cn-hangzhou
&ContactGroupName=TestGroup
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SearchAlertContactGroupResponse>
  <ContactGroups>
        <ContactGroupId>746</ContactGroupId>
        <UpdateTime>1529668855000</UpdateTime>
        <ContactGroupName>TestGroup</ContactGroupName>
        <UserId>113197164949****</UserId>
        <CreateTime>1529668855000</CreateTime>
  </ContactGroups>
  <ContactGroups>
        <Contacts>
              <Email>someone@example.com</Email>
              <UserId>113197164949****</UserId>
              <Phone>1381111*****</Phone>
              <CreateTime>1572349025000</CreateTime>
              <UpdateTime>1580258717000</UpdateTime>
              <ContactId>123</ContactId>
              <DingRobot>https://oapi.dingtalk.com/robot/send?access_token=91f2f6****</DingRobot>
              <SystemNoc>false</SystemNoc>
              <ContactName>John Doe</ContactName>
        </Contacts>
  </ContactGroups>
  <RequestId>4D6C358A-A58B-4F4B-94CE-F5AAF023****</RequestId>
</SearchAlertContactGroupResponse>
```

`JSON` 格式

```
{
    "ContactGroups": [
        {
            "ContactGroupId": 746,
            "UpdateTime": 1529668855000,
            "ContactGroupName": "TestGroup",
            "UserId": "113197164949****",
            "CreateTime": 1529668855000
        },
        {
            "Contacts": {
                "Email": "someone@example.com",
                "UserId": "113197164949****",
                "Phone": "1381111*****",
                "CreateTime": 1572349025000,
                "UpdateTime": 1580258717000,
                "ContactId": 123,
                "DingRobot": "https://oapi.dingtalk.com/robot/send?access_token=91f2f6****",
                "SystemNoc": false,
                "ContactName": "John Doe"
            }
        }
    ],
    "RequestId": "4D6C358A-A58B-4F4B-94CE-F5AAF023****"
}
```

