# ListDispatchRule

调用ListDispatchRule接口查询通知策略列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListDispatchRule&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListDispatchRule|系统规定参数。取值：ListDispatchRule。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Name|String|否|Prod|通知策略的名称， 支持模糊匹配。 |
|System|Boolean|否|true|-   `false`（默认）：通知策略为内部系统创建。
-   `true`：通知策略为外部系统创建。

**说明：** 外部系统创建的通知策略不支持在ARMS控制台修改通知策略的分派条件。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DispatchRules|Array of DispatchRule| |返回结构体。 |
|Name|String|Prod|通知策略的名称。 |
|RuleId|Long|10282|通知策略ID。 |
|State|String|true|通知策略的启用状态。

 -   `true`：启用。
-   `false`：关闭。 |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListDispatchRule
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListDispatchRuleResponse>
  <RequestId>34ED024E-9E31-434A-9E4E-D9D15C3****	</RequestId>
  <DispatchRules>
        <State>true</State>
        <RuleId>10282</RuleId>
        <Name>Prod</Name>
  </DispatchRules>
</ListDispatchRuleResponse>
```

`JSON`格式

```
{
    "RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3****",
    "DispatchRules": {
        "State": true,
        "RuleId": 10282,
        "Name": "Prod"
    }
}
```

