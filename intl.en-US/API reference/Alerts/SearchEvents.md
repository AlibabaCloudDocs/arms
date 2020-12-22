# SearchEvents

You can call this operation to query alert event records.

Alarm event records, not alarms. Is the event record after the alarm rule polls every minute. The service role. Valid values: triggered and untriggered. If the triggered event is not in the silence period, it will be sent.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=SearchEvents&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchEvents|The parameter specified by the system. Valid values: `SearchEvents` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |
|AlertId|Long|No|123|The ID of the alarm rule. You can call the SearchAlertRules operation to query the `Id` \), please refer to [SearchAlertRules](~~175825~~) . |
|Pid|String|No|atc889zkcf@d8deedfa9bf\*\*\*\*|Application ID\(PID\) of the application associated with the alarm |
|CurrentPage|Integer|No|1|The number of the page to return. The default is `1` . |
|PageSize|Integer|No|10|The number of items displayed on each page. The default is `10` . |
|AppType|String|No|TRACE|The type of the application associated with the alert rule. Valid values:

 -   `TRACE` : Application Monitoring
-   `RETCODE` : browser monitoring |
|AlertType|Integer|No|4|The type of the alarm rule. Valid values:

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus monitoring alarm rules. |
|IsTrigger|Integer|No|1|Indicates whether the alert event is triggered. If this parameter is not specified, all alert events are queried.

 -   `1` : trigger
-   `0` : not triggered |
|StartTime|Long|No|1595565300000|The timestamp of the start time for querying alert events. The format is Unix Timestamp Long, in milliseconds. The default value is 10 minutes before the current time. |
|EndTime|Long|No|1595568970000|The timestamp of the end time of query results. The format is Unix Timestamp Long, in milliseconds. The time to test rules. The default value is the current time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsTrigger|Integer|0|Internal parameters |
|PageBean|Struct| |The returned data struct. |
|Event|Array| |The alarm event list |
|AlertId|Long|123|The ID of the alert rule associated with the event. |
|AlertName|String|alertName|The name of the alert rule associated with the event. |
|AlertRule|String|\{\\"operator\\":\\"&\\",\\"rules\\":\[\{\\"aggregators \\":\\"AVG\\",\\"alias\\":\\"jvm\_threads \\",\\"measure\\":\\"appstat.jvm.ThreadCount\\",\\"nValue\\":1,\\"operator\\":\\"HOH\_DOWN\\",\\"value\\":50.0\}\]\}|The judgment condition configuration of the event-associated alarm rule. |
|AlertType|Integer|4|Event-associated alert rule type \(not displayed in most cases\):

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus monitoring alarm rules. |
|EventLevel|Integer|1|Event Level |
|EventTime|Long|1595569020000|The timestamp when the event occurred. |
|Id|Long|123|Event Record ID |
|Links|List|\[ "http://arms.console.aliyun.com/apm?spm=arms.alert.link&pid=xxxx@xxxx&regionId=cn-hangzhou\#/xxx@xxx/txn/\{\\"rpc\\":\\"/demo/queryNotExistDB/11\\",\\"tabs\\":\\"ov\\"\}" \]|Event restore onsite link list |
|Message|String|\{\\"Interface name: /demo/queryNotExistDB/11 \\":\\"application call statistics interface name: /demo/queryNotExistDB/11 call response time\_Ms\_last 5 minutes Average <2000.0, current value 25.8000\\", "event logs are too many to fully display \\":\\"... \\"\}|The event content in the JSONString format. The key indicates the dimension and the value indicates the alert content under the dimension. |
|PageNumber|Integer|1|The number of the page to return. |
|PageSize|Integer|10|The number of projects that are displayed on each page. |
|TotalCount|Integer|1|The total number of entries returned. |
|RequestId|String|32940175-181B-4B93-966E-4BB69176\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=SearchEvents &RegionId=cn-hangzhou &AlertId=123 &StartTime=1579499026000 &EndTime=1579499626000 &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <SearchEventsResponse> <PageBean> <TotalCount> 2 </TotalCount> <PageSize> 10 </PageSize> <PageNumber> 1 </PageNumber> <Event> <EventLevel> WARN </EventLevel> <AlertId> 123 </AlertId> <AlertName> alertname </AlertName> <Message> {"node IP address: 172.27.XX. XX" "JVM Monitoring node IP: 172. 27.xx. XX calculate the average decline from the previous hour to the last hour has not exceeded 50.0%","there are too many event logs, and the average decline is not fully displayed":"......"} </Message> <EventTime> 1595569020000 </EventTime> <Links> http://arms.console.aliyun.com/apm?startTime=1595565300000&endTime=1595569246633&regionId=cn-hangzhou&pid= ###* </Links> <AlertRule> {"operator":"&","rules":[{"aggregators":"AVG","alias":"jvm_threads","measure":"appstat.jvm.ThreadCount","nValue":1,"operator":"HOH_DOWN","value":50.0}]} </AlertRule> </Event> </PageBean> <RequestId> 32940175-181 B- 4B93-966E-4BB69176 **** </RequestId> </SearchEventsResponse> 
   
```

`JSON`

```

     {"PageBean": { "TotalCount": 2, "PageSize": 10, "PageNumber": 1, "Event": [ { "EventLevel": "WARN", "AlertId": 123, "AlertName": "alertName", "Message": "{\" Node IP: 172.27.XX. XX \":\" JVM Monitoring node IP: 172.27.XX. XX returns the average decrease over the previous hour for the last 1 minute, not exceeding 50.0%\",\" too many event logs, not fully displayed \":\" ....... \"}", "EventTime": 1595569020000, "Links": [ " http://arms.console.aliyun.com/apm?startTime=1595565300000&endTime=1595569246633&regionId=cn-hangzhou&pid= ###* " ], " AlertRule ": "{\"operator\":\"&\",\"rules\":[{\"aggregates\":\"AVG\",\"alias\":\"JVM_ total threads \",\"measure\":\"appstat.jvm.ThreadCount\",\"nValue\":1,\"operator\":\"HOH_DOWN\",\"value\":50.0}]}"}, " RequestId ": " 32940175-181 B- 4B93-966E-4BB69176 access_id * "} 
   
```

