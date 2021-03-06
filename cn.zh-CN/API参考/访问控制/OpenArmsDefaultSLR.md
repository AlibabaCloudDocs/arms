# OpenArmsDefaultSLR

调用OpenArmsDefaultSLR接口开通ARMS服务关联角色AliyunServiceRoleForARMS。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=OpenArmsDefaultSLR&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|OpenArmsDefaultSLR|系统规定参数。取值：OpenArmsDefaultSLR。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|true|操作是否成功。取值：

 -   `true`：成功。
-   `false`：失败。 |
|RequestId|String|53CACA70-2CF7-490C-BD06-1A2AE4EB\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=OpenArmsDefaultSLR
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<OpenArmsDefaultSLRResponse>
  <RequestId>53CACA70-2CF7-490C-BD06-1A2AE4EB****</RequestId>
  <Data>true</Data>
</OpenArmsDefaultSLRResponse>
```

`JSON`格式

```
{
    "RequestId": "53CACA70-2CF7-490C-BD06-1A2AE4EB****",
    "Data": true
}
```

