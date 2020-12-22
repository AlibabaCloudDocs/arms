# ListTraceApps

You can call this operation to query all application monitoring tasks in a specified region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=ListTraceApps&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTraceApps|The parameter specified by the system. Valid values: `ListTraceApps` . |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|Integer|200|Interface status code:

 -   `2XX` : successful
-   `3XX` : redirection
-   `4XX` : request error
-   `5XX` : Server error |
|Message|String|true|The information returned. |
|RequestId|String|40B10E04-81E8-4643-970D-F1B38F2E\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the operation is successful. Valid values:

 -   `true` : Operation succeeded
-   `false` : Operation failed |
|TraceApps|Array| |The list of returned application monitoring. |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application monitored. |
|CreateTime|Long|1529667762000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|atc889zkcf@d8deedfa9bfxxxx|The PID of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Specifies whether to be displayed in the console. |
|Type|String|TRACE|The type of the monitoring task. Valid values:

 -   `TRACE` : Application Monitoring
-   `RETCODE` : browser monitoring |
|UpdateTime|Long|1529667762000|The timestamp when the application was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=ListTraceApps &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <ListTraceAppsResponse> <TraceApps> <Type>TRACE</Type> <AppId>123</AppId> <UserId>113197164949****</UserId> <CreateTime>1571865746000</CreateTime> <UpdateTime>1571865746000</UpdateTime> <Pid>b590lhguqs@50e2179afeb****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app</AppName> </TraceApps> <TraceApps> <Type>TRACE</Type> <AppId>234</AppId> <UserId>113197164949****</UserId> <CreateTime>1572401289000</CreateTime> <UpdateTime>1572401289000</UpdateTime> <Pid>b590lhguqs@b0175fb5bda****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app2</AppName> </TraceApps> <TraceApps> <Type>TRACE</Type> <AppId>345</AppId> <UserId>113197164949****</UserId> <CreateTime>1576338375000</CreateTime> <UpdateTime>1576338375000</UpdateTime> <Pid>b590lhguqs@3afb9343a31****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app3</AppName> </TraceApps> <RequestId>40B10E04-81E8-4643-970D-F1B38F2E****</RequestId> <Code>200</Code> <Success>true</Success> </ListTraceAppsResponse> 
   
```

`JSON`

```

     { "TraceApps": [ { "Type": "TRACE", "AppId": 123, "UserId": "113197164949****", "CreateTime": 1571865746000, "UpdateTime": 1571865746000, "Pid": "b590lhguqs@50e2179afeb****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app" }, { "Type": "TRACE", "AppId": 234, "UserId": "113197164949****", "CreateTime": 1572401289000, "UpdateTime": 1572401289000, "Pid": "b590lhguqs@b0175fb5bda****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app2" }, { "Type": "TRACE", "AppId": 345, "UserId": "113197164949****", "CreateTime": 1576338375000, "UpdateTime": 1576338375000, "Pid": "b590lhguqs@3afb9343a31****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app3" } ], "RequestId": "40B10E04-81E8-4643-970D-F1B38F2E****", "Code": 200, "Success": true } 
   
```

