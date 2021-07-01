# SearchTraceAppByName

Queries application monitoring jobs by application name.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByName&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByName|The operation that you want to perform. Set the value to `SearchTraceAppByName`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|No|test-app|The name of the application for which you want to query application monitoring jobs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F7781D4A-2818-41E7-B7BB-79D809E9\*\*\*\*|The ID of the request. |
|TraceApps|Array of TraceApp| |The information about the application monitoring job. |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application. |
|CreateTime|Long|1593486786000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|a5f9bdeb-2627-4dbe-9247-\*\*\*\*|The process identifier \(PID\) of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether the application is displayed in the Application Real-Time Monitoring Service \(ARMS\) console. Valid values:

 -   `true`: The application is displayed in the ARMS console.
-   `false`: The application is not displayed in the ARMS console. |
|Type|String|TRACE|The type of the monitoring job. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|UpdateTime|Long|1593486786000|The timestamp when the application was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchTraceAppByName
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

