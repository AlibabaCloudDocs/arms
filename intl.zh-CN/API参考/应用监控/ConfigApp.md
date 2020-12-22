# ConfigApp

调用ConfigApp接口打开或关闭应用监控的Agent总开关，或者查询Agent总开关的状态。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ConfigApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ConfigApp|系统规定参数，取值为`ConfigApp`。 |
|AppIds|String|是|abc@def,ghi@jkl|应用的ID标识串（PID）。多个PID以半角逗号（,）分隔。 |
|Enable|String|是|true|打开或关闭一个或多个应用的Agent总开关。关闭开关后即停止监控。如果不填写该参数，则表示查询目标应用当前的Agent总开关状态。

 -   `true`：打开Agent总开关
-   `false`：关闭Agent总开关 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|abc@def success\\nghi@jkl success\\n|操作是否成功或者目标应用的Agent总开关状态 |
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ConfigApp
&AppIds=abc@def,ghi@jkl
&Enable=true
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ConfigAppResponse>
	  <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId>
	  <Data>abc@def success
	ghi@jkl success
	</Data>
</ConfigAppResponse>
```

`JSON` 格式

```
{
    "RequestId": "16AF921B-8187-489F-9913-43C808B4****",
    "Data": "abc@def success\nghi@jkl success\n"
}
```

