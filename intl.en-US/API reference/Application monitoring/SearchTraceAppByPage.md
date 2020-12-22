# SearchTraceAppByPage

You can call this operation to query SearchTraceAppByPage application monitoring tasks by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByPage|The parameter specified by the system. Valid values: `SearchTraceAppByPage` . |
|PageNumber|Integer|Yes|1|The number of the page to return. Optional. The parameter value. If you do not set this parameter, the default value is `1` . |
|PageSize|Integer|Yes|10|The number of entries to return on each page. Optional. The parameter value. If you do not set this parameter, the default value is `10` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|Yes|test-app|The name of the application. Optional. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The returned page information. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|3|The sum of queries. |
|TraceApps|Array| |Application Monitoring Task information |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application monitored. |
|CreateTime|Long|1531291867000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|The PID of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether to display the following content:

 -   `true` : Display
-   `false` : not displayed |
|Type|String|TRACE|The type of the monitoring task. Valid values:

 -   `TRACE` : Application Monitoring
-   `RETCODE` : browser monitoring |
|UpdateTime|Long|1531291867000|The timestamp when the instance was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|RequestId|String|4B446DF2-3DDD-4B5B-8E3F-D5225120\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=SearchTraceAppByPage &PageNumber=1 &PageSize=10 &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <SearchTraceAppByPageResponse> <PageBean> <TotalCount>3</TotalCount> <TraceApps> <Type>TRACE</Type> <AppId>123</AppId> <UserId>113197164949****</UserId> <CreateTime>1571865746000</CreateTime> <UpdateTime>1571865746000</UpdateTime> <Pid>b590lhguqs@50e2179afeb****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app</AppName> </TraceApps> <TraceApps> <Type>TRACE</Type> <AppId>234</AppId> <UserId>113197164949****</UserId> <CreateTime>1572401289000</CreateTime> <UpdateTime>1572401289000</UpdateTime> <Pid>b590lhguqs@b0175fb5bda****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app2</AppName> </TraceApps> <TraceApps> <Type>TRACE</Type> <AppId>345</AppId> <UserId>113197164949****</UserId> <CreateTime>1576338375000</CreateTime> <UpdateTime>1576338375000</UpdateTime> <Pid>b590lhguqs@3afb9343a31****</Pid> <Show>true</Show> <RegionId>cn-hangzhou</RegionId> <AppName>test-app3</AppName> </TraceApps> <PageSize>10</PageSize> <PageNumber>1</PageNumber> </PageBean> <RequestId>4B446DF2-3DDD-4B5B-8E3F-D5225120****</RequestId> </SearchTraceAppByPageResponse> 
   
```

`JSON`

```

     { "PageBean": { "TotalCount": 3, "TraceApps": [ { "Type": "TRACE", "AppId": 123, "UserId": "113197164949****", "CreateTime": 1571865746000, "UpdateTime": 1571865746000, "Pid": "b590lhguqs@50e2179afeb****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app" }, { "Type": "TRACE", "AppId": 234, "UserId": "113197164949****", "CreateTime": 1572401289000, "UpdateTime": 1572401289000, "Pid": "b590lhguqs@b0175fb5bda****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app2" }, { "Type": "TRACE", "AppId": 345, "UserId": "113197164949****", "CreateTime": 1576338375000, "UpdateTime": 1576338375000, "Pid": "b590lhguqs@3afb9343a31****", "Show": true, "RegionId": "cn-hangzhou", "AppName": "test-app3" } ], "PageSize": 10, "PageNumber": 1 }, "RequestId": "4B446DF2-3DDD-4B5B-8E3F-D5225120****" } 
   
```

