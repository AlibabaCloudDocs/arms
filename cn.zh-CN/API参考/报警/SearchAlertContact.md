# SearchAlertContact

调用SearchAlertContact接口查询报警联系人。

************

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertContact|系统规定参数，取值为`SearchAlertContact`。 |
|ContactName|String|是|John Doe|报警联系人名称。非必填。 |
|CurrentPage|String|是|1|查询分页的当前页码。 |
|Email|String|是|someone@example.com|联系人邮箱地址。非必填。 |
|PageSize|String|是|20|查询分页的每页项目数量。 |
|Phone|String|是|1381111\*\*\*\*\*|报警联系人电话号码。非必填。 |
|RegionId|String|是|cn-hangzhou|地域ID。始终填写`cn-hangzhou`。 |
|ProxyUserId|String|否|1234123\*|内部参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回结构体 |
|Contacts|Array| |联系人对象列表 |
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
|PageNumber|Integer|1|返回结果的页码 |
|PageSize|Integer|10|返回结果的每页项目数量 |
|TotalCount|Integer|23|返回结果的总项数数量 |
|RequestId|String|21E85B16-75A6-429A-9F65-8AAC9A54\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchAlertContact
&ContactName=John Doe
&CurrentPage=1
&Email=someone@example.com
&PageSize=20
&Phone=1381111*****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SearchAlertContactResponse>
	  <PageBean>
		    <TotalCount>2</TotalCount>
		    <PageSize>10</PageSize>
		    <Contacts>
			      <Email>someone1@example.com</Email>
			      <UserId>113197164949****</UserId>
			      <Phone>1381111*****</Phone>
			      <CreateTime>1572349025000</CreateTime>
			      <UpdateTime>1580258717000</UpdateTime>
			      <ContactId>123</ContactId>
			      <DingRobot>https://oapi.dingtalk.com/robot/send?access_token=91f2f6****</DingRobot>
			      <ContactName>John Doe</ContactName>
			      <SystemNoc>true</SystemNoc>
		    </Contacts>
		    <Contacts>
			      <Email>someone2@example.com</Email>
			      <Phone>1381111*****</Phone>
			      <UserId>113197164949****</UserId>
			      <CreateTime>1595319998000</CreateTime>
			      <UpdateTime>1595319998000</UpdateTime>
			      <ContactId>456</ContactId>
			      <DingRobot></DingRobot>
			      <ContactName>Jane Doe</ContactName>
			      <SystemNoc>false</SystemNoc>
		    </Contacts>
		    <PageNumber>1</PageNumber>
	  </PageBean>
	  <RequestId>21E85B16-75A6-429A-9F65-8AAC9A54****</RequestId>
</SearchAlertContactResponse>
```

`JSON` 格式

```
{
	"PageBean": {
		"TotalCount": 2,
		"PageSize": 10,
		"Contacts": [
			{
				"Email": "someone1@example.com",
				"UserId": "113197164949****",
				"Phone": "1381111*****",
				"CreateTime": 1572349025000,
				"UpdateTime": 1580258717000,
				"ContactId": 123,
				"DingRobot": "https://oapi.dingtalk.com/robot/send?access_token=91f2f6****",
				"ContactName": "John Doe",
				"SystemNoc": true
			},
			{
				"Email": "someone2@example.com",
				"Phone": "1381111*****",
				"UserId": "113197164949****",
				"CreateTime": 1595319998000,
				"UpdateTime": 1595319998000,
				"ContactId": 456,
				"DingRobot": "",
				"ContactName": "Jane Doe",
				"SystemNoc": false
			}
		],
		"PageNumber": 1
	},
	"RequestId": "21E85B16-75A6-429A-9F65-8AAC9A54****"
}
```

