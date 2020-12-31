# DeleteAlertRules

调用DeleteAlertRules接口删除报警规则。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteAlertRules&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAlertRules|系统规定参数，取值为`DeleteAlertRules`。 |
|AlertIds|String|是|\[123, 234\]|要删除的报警规则ID列表。格式为JSONArray，例如：`[123, 234]`。可调用SearchAlertRules接口获取报警规则ID（对应返回参数中的`Id`），详情请参见[SearchAlertRules](~~175825~~)。 |
|RegionId|String|是|cn-hangzhou|地域ID。默认为`cn-hangzhou`。 |
|ProxyUserId|String|否|123412\*\*|内部参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsSuccess|Boolean|true|删除报警规则是否成功。

 -   `true`：删除成功
-   `false`：删除失败 |
|RequestId|String|C21AB7CF-B7AF-410F-BD61-82D1567F\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteAlertRules
&AlertIds=[123, 234]
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteAlertRulesResponse>
	  <IsSuccess>true</IsSuccess>
	  <RequestId>C21AB7CF-B7AF-410F-BD61-82D1567F****</RequestId>
</DeleteAlertRulesResponse>
```

`JSON` 格式

```
{
    "IsSuccess": true,
    "RequestId": "C21AB7CF-B7AF-410F-BD61-82D1567F****"
}
```

