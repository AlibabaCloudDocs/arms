# UpdateWebhook

调用UpdateWebhook接口修改Webhook告警联系人信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=UpdateWebhook&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateWebhook|系统规定参数。取值：UpdateWebhook。 |
|ContactId|Long|是|48716|Webhook告警联系人ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|ContactName|String|否|Webhook告警|自定义联系人名称。 |
|Method|String|否|Post|HTTP请求方法。

 -   `Get`
-   `Post` |
|Url|String|否|https://oapi.dingtalk.com/robot/send?access\_token=e1a049121ddbfce1ca963d115ef88cc7219583c4fb79fe6e398fbfb688\*\*\*\*\*\*|**Method**的请求方法URL。 |
|HttpParams|String|否|\[\{"name":"mike"\}\]|HTTP请求参数。 |
|HttpHeaders|String|否|\[\{"Content-Type":"application/json"\}\]|HTTP请求头。 |
|Body|String|否|\{"msg\_type": "text","content": \{"text": "$content"\}\}|请求体。当**Method**设置为**Post**时必填，可在Body字符串中使用$content占位符输出告警内容。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsSuccess|Boolean|true|请求结果。

 -   `true`：修改成功。
-   `false`：修改失败。 |
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateWebhook
&ContactId=48716
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<UpdateWebhookResponse>
  <IsSuccess>true</IsSuccess>
  <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId>
</UpdateWebhookResponse>
```

`JSON`格式

```
{
    "IsSuccess": true,
    "RequestId": "16AF921B-8187-489F-9913-43C808B4****"
}
```

