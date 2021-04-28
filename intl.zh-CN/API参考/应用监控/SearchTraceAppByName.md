# SearchTraceAppByName

调用SearchTraceAppByName接口来按应用名称查询应用监控任务。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByName&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchTraceAppByName|系统规定参数，取值为`SearchTraceAppByName`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|TraceAppName|String|否|test-app|应用名称。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|F7781D4A-2818-41E7-B7BB-79D809E9\*\*\*\*|请求ID。 |
|TraceApps|Array of TraceApp| |应用监控任务信息。 |
|AppId|Long|123|应用ID。 |
|AppName|String|test-app|应用名称。 |
|CreateTime|Long|1593486786000|创建时间的时间戳。 |
|Labels|List|prod|应用标签。 |
|Pid|String|a5f9bdeb-2627-4dbe-9247-\*\*\*\*|应用的ID标识串。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|Show|Boolean|true|ARMS控制台中是否显示该应用：

 -   `true`：显示。
-   `false`：不显示。 |
|Type|String|TRACE|监控任务类型：

 -   `TRACE`：应用监控。
-   `RETCODE`：前端监控。 |
|UpdateTime|Long|1593486786000|更新时间的时间戳。 |
|UserId|String|113197164949\*\*\*\*|用户ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchTraceAppByName
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchTraceAppByNameResponse>
	  <TraceApps>
		    <Type>TRACE</Type>
		    <AppId>123</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1593486786000</CreateTime>
		    <UpdateTime>1593486786000</UpdateTime>
		    <Pid>a5f9bdeb-2627-4dbe-9247-****</Pid>
		    <Show>true</Show>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app</AppName>
	  </TraceApps>
	  <TraceApps>
		    <Type>TRACE</Type>
		    <AppId>234</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1594370374000</CreateTime>
		    <UpdateTime>1594370374000</UpdateTime>
		    <Pid>be1f9a33-9c8e-445e-9115-****</Pid>
		    <Show>true</Show>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app2</AppName>
	  </TraceApps>
	  <RequestId>F7781D4A-2818-41E7-B7BB-79D809E9****</RequestId>
</SearchTraceAppByNameResponse>
```

`JSON`格式

```
{
	"TraceApps": [
		{
			"Type": "TRACE",
			"AppId": 123,
			"UserId": "113197164949****",
			"CreateTime": 1593486786000,
			"UpdateTime": 1593486786000,
			"Pid": "a5f9bdeb-2627-4dbe-9247-****",
			"Show": true,
			"RegionId": "cn-hangzhou",
			"AppName": "test-app"
		},
		{
			"Type": "TRACE",
			"AppId": 234,
			"UserId": "113197164949****",
			"CreateTime": 1594370374000,
			"UpdateTime": 1594370374000,
			"Pid": "be1f9a33-9c8e-445e-9115-****",
			"Show": true,
			"RegionId": "cn-hangzhou",
			"AppName": "test-app2"
		}
	],
	"RequestId": "F7781D4A-2818-41E7-B7BB-79D809E9****"
}
```

