# StartAlert

调用StartAlert接口启动报警规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=StartAlert&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|StartAlert|系统规定参数，取值为`StartAlert`。 |
|AlertId|String|是|1610\*\*\*|报警规则ID，可调用SearchAlertRules接口查询，对应返回参数`Id`，详情请参见[SearchAlertRules](~~175825~~)。 |
|RegionId|String|是|cn-hangzhou|地域ID。始终填写`cn-hangzhou`。 |
|ProxyUserId|String|否|123412\*\*|内部参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsSuccess|Boolean|true|操作是否成功：

 -   `true`：操作成功
-   `false`：操作失败 |
|RequestId|String|27E653FA-5958-45BE-8AA9-14D884DC\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=StartAlert
&AlertId=1610***
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<StartAlertResponse>
	  <IsSuccess>true</IsSuccess>
	  <RequestId>27E653FA-5958-45BE-8AA9-14D884DC****</RequestId>
</StartAlertResponse>
```

`JSON` 格式

```
{
    "IsSuccess": true,
    "RequestId": "27E653FA-5958-45BE-8AA9-14D884DC****"
}
```

