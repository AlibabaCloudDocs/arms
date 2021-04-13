# DeletePrometheusAlertRule

调用DeletePrometheusAlertRule接口删除Prometheus告警规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeletePrometheusAlertRule&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeletePrometheusAlertRule|系统规定参数。取值：DeletePrometheusAlertRule。 |
|AlertId|Long|是|3888704|告警规则ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|请求ID。 |
|Success|Boolean|true|是否删除成功。取值：

 -   `true`：删除成功
-   `false`：删除失败 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeletePrometheusAlertRule
&AlertId=3888704
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeletePrometheusAlertRuleResponse>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
  <Success>true</Success>
</DeletePrometheusAlertRuleResponse>
```

`JSON`格式

```
{
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****",
    "Success": true
}
```

