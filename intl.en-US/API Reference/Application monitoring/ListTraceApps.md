# ListTraceApps

Queries all application monitoring tasks in a specified region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListTraceApps&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTraceApps|The operation that you want to perform. Set the value to `ListTraceApps`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|Integer|200|The HTTP status code returned for the request. Valid values:

 -   `2XX`: The request is successful.
-   `3XX`: A redirection message is returned.
-   `4XX`: The request is invalid.
-   `5XX`: A server error occurs. |
|Message|String|Internal error. Please try again. Contact the DingTalk service account if the issue persists after multiple retries.|The error message returned when the request parameters are invalid. |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the call is successful. Valid values:

 -   `true`: The call is successful.
-   `false`: The call fails. |
|TraceApps|Array of TraceApp| |The list of application monitoring tasks. |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application. |
|CreateTime|Long|1529667762000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|a5f9bdeb-2627-4dbe-9247-\*\*\*\*|The process identifier \(PID\) of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether the application is displayed in the Application Real-Time Monitoring Service \(ARMS\) console. Valid values:

 -   `true`: The application is displayed in the ARMS console.
-   `false`: The application is not displayed in the ARMS console. |
|Type|String|TRACE|The type of the monitoring task. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|UpdateTime|Long|1529667762000|The timestamp when the task was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=ListTraceApps
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

