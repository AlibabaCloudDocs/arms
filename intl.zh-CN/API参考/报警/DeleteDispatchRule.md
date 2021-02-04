# DeleteDispatchRule

调用DeleteDispatchRule接口删除指定ID的分派策略。

********

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteDispatchRule&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteDispatchRule|系统规定参数。取值：DeleteDispatchRule。 |
|Id|String|是|12345|分派策略ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|请求ID。 |
|Success|Boolean|true|是否删除成功。

 -   `true`删除成功
-   `false`删除失败 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteDispatchRule
&Id=12345
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteDispatchRuleResponse>
      <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId>
      <Success>true</Success>
</DeleteDispatchRuleResponse>
```

`JSON`格式

```
{
    "RequestId": "16AF921B-8187-489F-9913-43C808B4****",
    "Success": true
}
```

