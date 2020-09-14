# GetTraceApp

调用GetTraceApp接口获取应用监控任务详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetTraceApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetTraceApp|系统规定参数。取值：`GetTraceApp`。 |
|Pid|String|是|xxx@74xxx|应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/doc-detail/146244.htm#p-xyi-tr6-2w5)。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|CBFA2436-9453-4991-AC0E-9DC42A26\*\*\*\*|请求ID |
|TraceApp|Struct| |返回结构体 |
|AppId|Long|123|应用ID |
|AppName|String|test-app|应用名称 |
|CreateTime|Long|1529667762000|创建时间的时间戳 |
|Labels|List|prod|应用标签 |
|Pid|String|atc889zkcf@d8deedfa9bfxxxx|应用的ID标识串 |
|RegionId|String|cn-hangzhou|地域ID |
|Show|Boolean|true|是否显示 |
|Type|String|TRACE|监控任务类型：

 -   `TRACE`：应用监控
-   `RETCODE`：前端监控 |
|UpdateTime|Long|1529667762000|更新时间的时间戳 |
|UserId|String|113197164949\*\*\*\*|用户ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetTraceApp
&Pid=xxx@74xxx
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetTraceAppResponse>
	  <RequestId>CBFA2436-9453-4991-AC0E-9DC42A26****</RequestId>
	  <TraceApp>
		    <Type>TRACE</Type>
		    <AppId>123</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1529667762000</CreateTime>
		    <UpdateTime>1529667762000</UpdateTime>
		    <Pid>atc889zkcf@d8deedfa9bfxxxx</Pid>
		    <Show>true</Show>
		    <Labels>prod</Labels>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app</AppName>
	  </TraceApp>
</GetTraceAppResponse>
```

`JSON` 格式

```
{
    "RequestId": "CBFA2436-9453-4991-AC0E-9DC42A26****",
    "TraceApp": {
        "Type": "TRACE",
        "AppId": 123,
        "UserId": "113197164949****",
        "CreateTime": 1529667762000,
        "UpdateTime": 1529667762000,
        "Pid": "atc889zkcf@d8deedfa9bfxxxx",
        "Show": true,
        "Labels": "prod",
        "RegionId": "cn-hangzhou",
        "AppName": "test-app"
    }
}
```

