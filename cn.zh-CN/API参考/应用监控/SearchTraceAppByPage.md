# SearchTraceAppByPage

调用SearchTraceAppByPage接口来分页查询应用监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchTraceAppByPage|系统规定参数，取值为`SearchTraceAppByPage`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|TraceAppName|String|否|test-app|应用名称。 |
|PageNumber|Integer|否|1|查询结果的页码，如果不填写则默认为`1`。 |
|PageSize|Integer|否|10|查询结果的每页项目数量，如果不填写则默认为`10`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回的页面信息。 |
|PageNumber|Integer|1|返回结果的页码。 |
|PageSize|Integer|10|返回结果的每页项目数量。 |
|TotalCount|Integer|3|查询结果的总项目数量。 |
|TraceApps|Array of TraceApp| |应用监控任务信息。 |
|AppId|Long|123|应用ID。 |
|AppName|String|test-app|应用名称。 |
|CreateTime|Long|1531291867000|创建时间的时间戳。 |
|Labels|List|prod|应用标签。 |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|应用的ID标识串。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|Show|Boolean|true|是否在ARMS控制台显示：

 -   `true`：显示。
-   `false`：不显示。 |
|Type|String|TRACE|监控任务类型：

 -   `TRACE`：应用监控。
-   `RETCODE`：前端监控。 |
|UpdateTime|Long|1531291867000|更新时间的时间戳。 |
|UserId|String|113197164949\*\*\*\*|用户ID。 |
|RequestId|String|4B446DF2-3DDD-4B5B-8E3F-D5225120\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchTraceAppByPage
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchTraceAppByPageResponse>
	  <PageBean>
		    <TotalCount>3</TotalCount>
		    <TraceApps>
			      <Type>TRACE</Type>
			      <AppId>123</AppId>
			      <UserId>113197164949****</UserId>
			      <CreateTime>1571865746000</CreateTime>
			      <UpdateTime>1571865746000</UpdateTime>
			      <Pid>b590lhguqs@50e2179afeb****</Pid>
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
			      <Pid>b590lhguqs@b0175fb5bda****</Pid>
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
			      <Pid>b590lhguqs@3afb9343a31****</Pid>
			      <Show>true</Show>
			      <RegionId>cn-hangzhou</RegionId>
			      <AppName>test-app3</AppName>
		    </TraceApps>
		    <PageSize>10</PageSize>
		    <PageNumber>1</PageNumber>
	  </PageBean>
	  <RequestId>4B446DF2-3DDD-4B5B-8E3F-D5225120****</RequestId>
</SearchTraceAppByPageResponse>
```

`JSON`格式

```
{
	"PageBean": {
		"TotalCount": 3,
		"TraceApps": [
			{
				"Type": "TRACE",
				"AppId": 123,
				"UserId": "113197164949****",
				"CreateTime": 1571865746000,
				"UpdateTime": 1571865746000,
				"Pid": "b590lhguqs@50e2179afeb****",
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
				"Pid": "b590lhguqs@b0175fb5bda****",
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
				"Pid": "b590lhguqs@3afb9343a31****",
				"Show": true,
				"RegionId": "cn-hangzhou",
				"AppName": "test-app3"
			}
		],
		"PageSize": 10,
		"PageNumber": 1
	},
	"RequestId": "4B446DF2-3DDD-4B5B-8E3F-D5225120****"
}
```

