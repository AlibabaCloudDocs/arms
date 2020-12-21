# CreateAlertContact

调用CreateAlertContact接口创建报警联系人。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=CreateAlertContact&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAlertContact|系统规定参数。取值：CreateAlertContact。 |
|RegionId|String|是|cn-hangzhou|地域ID。始终填写`cn-hangzhou`。 |
|ContactName|String|否|JohnDoe|报警联系人名称。 |
|PhoneNum|String|否|1381111\*\*\*\*|联系人手机号码。PhoneNum、Email和DingRobotWebhookUrl必须至少填写一个。 |
|Email|String|否|someone@example.com|联系人邮箱地址。PhoneNum、Email和DingRobotWebhookUrl必须至少填写一个。 |
|DingRobotWebhookUrl|String|否|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|钉钉机器人Webhook URL，获取方式请参见[设置钉钉机器人报警](https://help.aliyun.com/document_detail/106247.html)。PhoneNum、Email和DingRobotWebhookUrl必须至少填写一个。

 **说明：** 钉钉机器人安全设置中的自定义关键词请填写`报警`。 |
|SystemNoc|Boolean|否|true|是否接收系统通知：

 -   `true`：接收系统通知
-   `false`：不接收系统通知 |

邮箱地址、手机号码和钉钉机器人 Webhook URL 这三种联系方式中必须至少填写一种。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ContactId|String|102\*\*|报警联系人ID。 |
|RequestId|String|E9C9DA3D-10FE-472E-9EEF-2D0A3E41\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateAlertContact
&ContactName=JohnDoe
&DingRobotWebhookUrl=https://oapi.dingtalk.com/robot/send?access_token=91f2f6****
&Email=someone@example.com
&PhoneNum=1381111****
&RegionId=cn-hangzhou
&SystemNoc=true
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateAlertContactResponse>
	  <RequestId>E9C9DA3D-10FE-472E-9EEF-2D0A3E41****</RequestId>
	  <ContactId>102**</ContactId>
</CreateAlertContactResponse>
```

`JSON` 格式

```
{
    "RequestId": "E9C9DA3D-10FE-472E-9EEF-2D0A3E41****",
    "ContactId": "102**"
}
```

