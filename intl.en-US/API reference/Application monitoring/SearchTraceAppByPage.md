# SearchTraceAppByPage

You can call this operation to query application monitoring jobs by page.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByPage|The operation that you want to perform. Set this value to `SearchTraceAppByPage`. |
|PageNumber|Integer|Yes|1|The number of the page to return. |
|PageSize|Integer|Yes|2|The number of entries to return on each page. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|Yes|Demo|The name of application for which you want to query the application monitoring jobs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean| | |The information returned on the page that you queried. |
|PageNumber|Integer|1|The number of the page returned. |
|PageSize|Integer|2|The number of entries returned on each page. |
|TotalCount|Integer|22|The total number of entries returned. |
|TraceApps| | |The information about the application monitoring jobs. |
|AppId|Long|6549|The ID of the application monitored. |
|AppName|String|4123-docker-demo|The name of the application monitored. |
|CreateTime|Long|1531291867000|The time when the application monitoring job was created. |
|Pid|String|xxxxxxxxxxxxxxx|The PID. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Type|String|TRACE|The monitoring type. |
|UpdateTime|Long|1531291867000|The time when the application monitoring job was updated. |
|UserId|String|xxxxxxxxxxxx|The ID of the user. |
|RequestId|String|18B01385-A3B9-4BCF-988A-2064D77CF2C7|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/trace/SearchTraceAppByPage.json?PageNumber=1
&PageSize=2
&RegionId=cn-hangzhou
&TraceAppName=Demo

```

Sample success response

`XML` format

```
<SearchTraceAppByPage>
       <RequestId>18B01385-A3B9-4BCF-988A-2064D77CF2C7</RequestId>
       <PageBean>
              <PageNumber>1</PageNumber>
              <PageSize>2</PageSize>
              <TotalCount>22</TotalCount>
              <TraceApps>
                     <TraceApp>
                            <AppId>6549</AppId>
                            <AppName>4123-docker-demo</AppName>
                            <CreateTime>1531291867000</CreateTime>
                            <Pid>xxxxxxxxxxxxxxxxxx</Pid>
                            <RegionId>cn-hangzhou</RegionId>
                            <Type>TRACE</Type>
                            <UpdateTime>1531291867000</UpdateTime>
                            <UserId>xxxxxxxxxxxx</UserId>
                     </TraceApp>
                     <TraceApp>
                            <AppId>10198</AppId>
                            <AppName>132-k8s-demo</AppName>
                            <CreateTime>1540189384000</CreateTime>
                            <Pid>xxxxxxxxxxxxxxxxxxxxx</Pid>
                            <RegionId>cn-hangzhou</RegionId>
                            <Type>TRACE</Type>
                            <UpdateTime>1540189384000</UpdateTime>
                            <UserId>xxxxxxxxxxxx</UserId>
                     </TraceApp>
              </TraceApps>
       </PageBean>
</SearchTraceAppByPage>
```

`JSON` format

```
{
	"pageBean":{
		"traceApps":[
			{
				"appName":"4123-docker-demo",
				"createTime":1531291867000,
				"appId":6549,
				"updateTime":1531291867000,
				"userId":"xxxxxxxxxxxx",
				"pid":"xxxxxxxxxxxxxxxxxx",
				"type":"TRACE",
				"regionId":"cn-hangzhou",
			},
			{
				"appName":"132-k8s-demo",
				"createTime":1540189384000,
				"appId":10198,
				"updateTime":1540189384000,
				"userId":"xxxxxxxxxxxx",
				"pid":"xxxxxxxxxxxxxxxxxxxxx",
				"type":"TRACE",
				"regionId":"cn-hangzhou"
			}
		],
		"totalCount":22,
		"pageSize":2,
		"pageNumber":1
	},
	"requestId":"18B01385-A3B9-4BCF-988A-2064D77CF2C7"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

