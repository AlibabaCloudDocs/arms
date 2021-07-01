# SearchTraceAppByPage

Queries application monitoring jobs by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByPage|The operation that you want to perform. Set the value to `SearchTraceAppByPage`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|No|test-app|The name of the application. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: `1`. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: `10`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The information returned on the current page. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|3|The total number of entries returned. |
|TraceApps|Array of TraceApp| |The information about the application monitoring job. |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application. |
|CreateTime|Long|1531291867000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|The process identifier \(PID\) of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether the application is displayed in the Application Real-Time Monitoring Service \(ARMS\) console. Valid values:

 -   `true`: The application is displayed in the ARMS console.
-   `false`: The application is not displayed in the ARMS console. |
|Type|String|TRACE|The type of the monitoring job. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|UpdateTime|Long|1531291867000|The timestamp when the application was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|RequestId|String|4B446DF2-3DDD-4B5B-8E3F-D5225120\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchTraceAppByPage
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

