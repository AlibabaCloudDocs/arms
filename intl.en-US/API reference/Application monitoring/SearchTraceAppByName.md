# SearchTraceAppByName

You can call this operation to query SearchTraceAppByName tasks by Application Monitoring name.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByName&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByName|The parameter specified by the system. Valid values: `SearchTraceAppByName` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|Yes|test-app|The name of the application. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F7781D4A-2818-41E7-B7BB-79D809E9\*\*\*\*|The ID of the request. |
|TraceApps|Array| |Application Monitoring Task information |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application monitored. |
|CreateTime|Long|1593486786000|The timestamp when the instance was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|The PID of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether to display the following content:

 -   `true` : Display
-   `false` : not displayed |
|Type|String|TRACE|The type of the monitoring task. Valid values:

 -   `TRACE` : Application Monitoring
-   `RETCODE` : browser monitoring |
|UpdateTime|Long|1593486786000|The timestamp when the instance was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=SearchTraceAppByName &RegionId=cn-hangzhou &TraceAppName=test-app &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <SearchTraceAppByNameResponse> <TraceApps> <Type>TRACE</Type> <AppId>123</AppId> <UserId>113197164949****</UserId> <CreateTime>1593486786000</CreateTime> <UpdateTime>1593486786000</UpdateTime> <Pid>b590lhguqs@b071c539188****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app</AppName> </TraceApps> <TraceApps> <Type>TRACE</Type> <AppId>234</AppId> <UserId>113197164949****</UserId> <CreateTime>1594370374000</CreateTime> <UpdateTime>1594370374000</UpdateTime> <Pid>b590lhguqs@bcef83db34b****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app2</AppName> </TraceApps> <RequestId>F7781D4A-2818-41E7-B7BB-79D809E9****</RequestId> </SearchTraceAppByNameResponse> 
   
```

`JSON`

```

     { "TraceApps": [ { "Type": "TRACE", "AppId": 123, "UserId": "113197164949****", "CreateTime": 1593486786000, "UpdateTime": 1593486786000, "Pid": "b590lhguqs@b071c539188****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app" }, { "Type": "TRACE", "AppId": 234, "UserId": "113197164949****", "CreateTime": 1594370374000, "UpdateTime": 1594370374000, "Pid": "b590lhguqs@bcef83db34b****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app2" } ], "RequestId": "F7781D4A-2818-41E7-B7BB-79D809E9****" } 
   
```

