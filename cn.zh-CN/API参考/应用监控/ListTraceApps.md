# ListTraceApps

调用ListTraceApps接口获取指定地域下全部应用监控任务的列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListTraceApps&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTraceApps|系统规定参数，取值为`ListTraceApps`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|Integer|200|接口状态码：

 -   `2XX`：成功
-   `3XX`：重定向
-   `4XX`：请求错误
-   `5XX`：服务器错误 |
|Message|String|Internal error. Please try again. Contact the DingTalk service account if the issue persists after multiple retries.|请求参数错误时返回的信息 |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|请求ID |
|Success|Boolean|true|操作是否成功：

 -   `true`：操作成功
-   `false`：操作失败 |
|TraceApps|Array of TraceApp| |返回的应用监控列表信息 |
|AppId|Long|123|应用ID |
|AppName|String|test-app|应用名称 |
|CreateTime|Long|1529667762000|创建时间的时间戳 |
|Labels|List|prod|应用标签 |
|Pid|String|a5f9bdeb-2627-4dbe-9247-\*\*\*\*|应用的ID标识串 |
|RegionId|String|cn-hangzhou|地域ID |
|Show|Boolean|true|ARMS控制台是否显示该应用：

 -   `true`：显示
-   `false`：不显示 |
|Type|String|TRACE|监控任务类型：

 -   `TRACE`：应用监控
-   `RETCODE`：前端监控 |
|UpdateTime|Long|1529667762000|更新时间的时间戳 |
|UserId|String|113197164949\*\*\*\*|用户ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListTraceApps
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListTraceAppsResponse>
	  <TraceApps>
		    <Type>TRACE</Type>
		    <AppId>123</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1571865746000</CreateTime>
		    <UpdateTime>1571865746000</UpdateTime>
		    <Pid>a5f9bdeb-2627-4dbe-9247-****</Pid>
		    <Show>true</Show>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app</AppName>
	  </TraceApps>
	  <TraceApps>
		    <Type>TRACE</Type>
		    <AppId>234</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1572401289000</CreateTime>
		    <UpdateTime>1572401289000</UpdateTime>
		    <Pid>be1f9a33-9c8e-445e-9115-****</Pid>
		    <Show>true</Show>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app2</AppName>
	  </TraceApps>
	  <TraceApps>
		    <Type>TRACE</Type>
		    <AppId>345</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1576338375000</CreateTime>
		    <UpdateTime>1576338375000</UpdateTime>
		    <Pid>e04391e2-a7e0-4fbe-9987****</Pid>
		    <Show>true</Show>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app3</AppName>
	  </TraceApps>
	  <RequestId>40B10E04-81E8-4643-970D-F1B38F2E****</RequestId>
	  <Code>200</Code>
	  <Success>true</Success>
</ListTraceAppsResponse>
```

`JSON`格式

```
{
	"TraceApps": [
			{
				"Type": "TRACE",
				"AppId": 123,
				"UserId": "113197164949****",
				"CreateTime": 1571865746000,
				"UpdateTime": 1571865746000,
				"Pid": "a5f9bdeb-2627-4dbe-9247-****",
				"Show": true,
				"RegionId": "cn-hangzhou",
				"AppName": "test-app"
			},
			{
				"Type": "TRACE",
				"AppId": 234,
				"UserId": "113197164949****",
				"CreateTime": 1572401289000,
				"UpdateTime": 1572401289000,
				"Pid": "be1f9a33-9c8e-445e-9115-****",
				"Show": true,
				"RegionId": "cn-hangzhou",
				"AppName": "test-app2"
			},
			{
				"Type": "TRACE",
				"AppId": 345,
				"UserId": "113197164949****",
				"CreateTime": 1576338375000,
				"UpdateTime": 1576338375000,
				"Pid": "e04391e2-a7e0-4fbe-9987-****",
				"Show": true,
				"RegionId": "cn-hangzhou",
				"AppName": "test-app3"
			}
		],
	"RequestId": "40B10E04-81E8-4643-970D-F1B38F2E****",
	"Code": 200,
	"Success": true
}
```

