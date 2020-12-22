# SearchAlertRules

Call the SearchAlertRules API to query alarm rules.

**** **** ****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=SearchAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertRules|The parameter specified by the system. Valid values: `SearchAlertRules` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |
|Title|String|No|AlertRuleTitle|The name of the alert rule. |
|Type|String|No|4|The type of the alarm rule. Valid values:

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus monitoring alarm rules. |
|CurrentPage|Integer|No|1|The number of the page to return. The default is `1` . |
|PageSize|Integer|No|20|The number of items displayed on each page. The default is `10` . |
|Pid|String|No|atc889zkcf@d8deedfa9bf\*\*\*\*|The ID of the ARMS application associated with the alert rule. Alert types include:

 -   Application Monitoring the Pid corresponding to the alert rule.
-   Pid of the site corresponding to the browser monitoring alarm rule |
|AppType|String|No|TRACE|The application type of the alert rule. Valid values:

 -   `TRACE` : application monitoring alarm rule
-   `RETCODE` : browser monitoring alarm rules |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |Returns a structure. |
|AlertRules|Array| |The information about alert rules. |
|AlarmContext|Struct| |The format of the alert message. |
|AlarmContentSubTitle|String|TestSubTitle|The sub-title of the alarm content. |
|AlarmContentTemplate|String|Alarm name: $alarm name \\n filter condition: $filter \\n alarm time: $alarm time \\n alarm content: $alarm content \\n Note: The alarm is being triggered continuously until an email is received for recovery \\n 24 hours later, the system will remind you again!|Alarm notification content template. |
|AlertLevel|String|WARN|The notification level. Currently, only notification levels are supported . `WARN` . |
|AlertRule|Struct| |The list of judgment conditions for the alert rule. Multiple conditions can be separated by logical and logical operators or logical or operators. |
|Operator|String|\||Alarm rule judgment logic. `&` Represents the and logic, `|` Indicates the or logic. |
|Rules|Array| |The judgment conditions of the alarm rules. |
|Aggregates|String|AVG|Aggregation logic of alarm detection rules:

 -   `AVG` : averaging every minute
-   `SUM` : sum every minute .
-   `MAX` : maximum value per minute
-   `MIN` : minimum value per minute |
|Alias|String|Response time\_ms|The text for displaying the alarm metric. |
|Measure|String|appstat.jvm.SystemDiskFree|Alarm rule data metrics, based on which determine whether alarm rule conditions are met. For more information, see **alarm indicator value enumeration**. . |
|NValue|Integer|5|The range of request data in the judgment conditions of an alert rule. Unit: minutes. For example, NValue=5 indicates that the alarm per minute will request data for the last 5 minutes. |
|Operator|String|CURRENT\_GTE|The judgment symbol for the judgment condition of an alarm rule:

 -   CURRENT\_GTE: greater than or equal to
-   CURRENT\_LTE: less than or equal to
-   PREVIOUS\_UP: The month-on-month increase percentage.
-   PREVIOUS\_DOWN: The mom decrease percentage.
-   HOH\_UP: the increase percentage compared with the previous hour.
-   HOH\_DOWN: decrease percentage compared with the previous hour
-   DOD\_UP: increase in percentage compared with yesterday
-   Doc\_down: decrease percentage compared with yesterday |
|Value|Float|30|The judgment threshold of the judgment condition of the alarm rule. |
|AlertTitle|String|TestAlertRule|The name of the alert rule. |
|AlertType|Integer|4|The type of the alarm rule. Valid values:

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus monitoring alarm rules. |
|AlertVersion|Integer|1|The version of the alert rule. The default version is `1` . |
|AlertWays|List|\["MAIL", "SMS", "DING\_ROBOT"\]|Alarm Notification sending method:

 -   `SMS` : SMS
-   `MAIL` : email
-   `DING_ROBOT` : DingTalk robot |
|Config|String|\{\\"continuous\\":true,\\"dataRevision\\":2\}|The configuration items of the alert rule. The value is a JSON-formatted string.

 **continuous** The values for include:

 -   `true` : sends an alarm every minute
-   `false` : turn on the alarm silence period switch

 **dataRevision** The policy when data is null or is not obtained. Valid values :

 -   `0` : zero fill policy.
-   `1` : make up one strategy.
-   `2` : returns a null value. If no data exists, no alert is triggered. Default value: null. |
|ContactGroupIdList|String|381\*,572\*|The ID of the Contact Group specified in the alert rule. Multiple IDs are separated with commas \(,\). |
|CreateTime|Long|1579508519683|The timestamp when the alert rule is created. |
|Id|Long|123|The ID of the alert rule. |
|MetricParam|Struct| |Configure the information of the application associated with the alert rule. |
|AppGroupId|String|DEFAULT|The ID of the application associated with the alarm sub group. This parameter is applicable to application grouping scenarios in EDAS. |
|AppId|String|123|The auto-increment ID of the ARMS application. You can ignore this ID. |
|Dimensions|Array| |The dimension in the alert rule judgment conditions. |
|Key|String|rootIp|The name of the dimension. Valid values:

 -   `rpc` : Interface name
-   `rpcType` : type of API call \(such as HTTP and DUBBO\)
-   `endpoint` : database name
-   `rootIp` : Machine IP |
|Type|String|DISABLED|The type of the dimension. Valid values:

 -   `STATIC` : fixed matching this dimension value needs to be set **dimensions.value** .
-   `ALL` : the interface name is included in the alarm content when the threshold value is determined based on all dimensions of this API in sequence. This parameter is not required . **dimensions.value** .
-   `DISABLE` : Aggregates All dimension values into one value \(summation\). In this case, you do not need to enter **dimensions.value**. . |
|Value|String|"127.0.0.1"|The value of the dimension option. |
|Pid|String|9870ca99-8105-4da7-a3a4-d72dd1b1\*\*\*\*|The ID of the application associated with the alert rule. |
|Type|String|DB|The metric type of the alert rule.

 -   `TXN` : Application Monitoring entry call volume
-   `TXN_TYPE` : application monitoring call type statistics .
-   `DB` : Database metrics
-   `JVM` : JVM Monitoring
-   `HOST` : host monitoring
-   `EXCEPTION` : abnormal interface call |
|Notice|Struct| |The effective time range and notification time range of the alert rule. |
|EndTime|Long|1480607940000|The end time of the time range during which the alert rules are applied. This parameter helps you distinguish between 24 hours in a day and 24 hours in an alert rule. The time is in UNIX timestamp format. Valid values: year, month, and day. Only the value of hour, minute, and second is valid. |
|NoticeEndTime|Long|1480607940000|The end of the time range for when an alert rule is notified. The time range defines the 24 hours of an alert rule in each day. The time is in UNIX timestamp format. Valid values: year, month, and day. Only the value of hour, minute, and second is valid. |
|NoticeStartTime|Long|1480521600000|The start time of the alert rule time range. This parameter sets the notification time range for 24 hours in a day. The time is in UNIX timestamp format. Valid values: year, month, and day. Only the value of hour, minute, and second is valid. |
|StartTime|Long|1480521600000|The start time of the alert rule time range. This parameter sets the effective time range for the alert rule in 24 hours every day. The time is in UNIX timestamp format. Valid values: year, month, and day. Only the value of hour, minute, and second is valid. |
|RegionId|String|cn-hangzhou|The region ID of the alert rule. |
|Status|String|RUNNING|The status of the alert rule. `RUNNING` Running : `STOPPED` Indicates stopped. |
|TaskId|Long|123|The ID of the ARMS task associated with the custom task-based monitoring alarm rule. |
|TaskStatus|String|""|The internal field. |
|UpdateTime|Long|1480521600000|The timestamp when the alarm rule is updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user to which the alert rule belongs. |
|PageNumber|Integer|1|The page number of the query result. |
|PageSize|Integer|20|The number of items displayed on each page. |
|TotalCount|Integer|23|The total number of entries returned. |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|The ID of the request. |

## Alarm metric value enumeration

-   metricParam.type: Set the alert type to TXN \(indicating the number of application monitoring inbound calls\).
    -   The type of alarm dimension \(dimensions.key\):rpc \(interface name\)
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.txn.rt: The entrance call response time in milliseconds.
        -   appstat.txn.count: the number of entry calls.
        -   appstat.txn.errcount: the number of entry call errors
-   metricParam.type: Set the alert type to TXN\_TYPE. The application monitoring call type is used.
    -   The alert dimension in this class \(dimensions.key\) is the rpcType \(type of API calls, such as HTTP and DUBBO\).
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.inbound.rt: the response time to service calls provided by the application, in milliseconds.
        -   appstat.inbound.count: the number of service calls provided by applications.
        -   appstat.inbound.error: the number of service call errors.
        -   appstat.outbound.rt: the response time \(MS\) for the call of application-dependent services
        -   appstat.outbound.count: the number of calls to the dependent services of the application
        -   appstat.outbound.error: the number of errors that the application depends on service call.
-   Alert type \(metricParam.type\):DB \(database metric\)
    -   The type of alarm dimension \(dimensions.key\):endpoint \(database name\)
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.database.rt: response time for database calls \(MS\)
        -   appstat.database.count: the number of database calls
        -   appstat.database.errcount: the number of database call errors
-   Alert type \(metricParam.type\):JVM\(JVM Monitoring\)
    -   The alarm dimension \(dimensions.key\): roottip \(machine IP address\).
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.jvm.heap\_used: total memory in the JVM heap \(in bytes\)
        -   appstat.jvm.GcPsScavengeCount:JVM GC times
        -   appstat.jvm.GcPsMarkSweepCount: the number of JVM mark deletions
        -   appstat.jvm.GcG1OldGenCount: the number of G1GC in JVM\_Old
        -   appstat.jvm.GcG1YoungGenCount: G1GC times in JVM\_Young area
        -   appstat.jvm.gc.YoungGcCountInstant:JVM\_YoungGC count
        -   appstat.jvm.gc.OldGcCountInstant:JVM\_FullGC count
        -   appstat.jvm.gc.YoungGcTimeInstant:JVM\_YoungGC elapsed time \(MS\)
        -   appstat.jvm.gc.OldGcTimeInstant:JVM\_FullGC time \(MS\)
        -   appstat.jvm.ThreadCount: total number of jvm\_threads
        -   appstat.jvm.non\_heap\_used: total JVM non-heap memory usage \(in bytes\)
        -   appstat.jvm.non\_heap\_max: maximum JVM non-heap memory \(in bytes\)
        -   appstat.jvm.non\_heap\_init: initial value of JVM non-heap memory \(bytes\)
        -   appstat.jvm.non\_heap\_committed: the submitted value of the JVM non-heap memory. Unit: bytes.
-   Alert type \(metricParam.type\):HOST \(HOST monitoring\)
    -   The alarm dimension \(dimensions.key\): roottip \(machine IP address\).
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.jvm.SystemCpuUser: Node User usage CPU \(percentage\)
        -   appstat.jvm.SystemMemFree: node machine idle memory \(bytes\)
        -   appstat.jvm.SystemDiskFree: node idle disk \(bytes\)
        -   appstat.jvm.SystemNetInErrs: node machine receives error messages
        -   appstat.jvm.SystemNetOutErrs: number of error messages sent by node machines
        -   appstat.jvm.SystemLoad: node machine system load
-   metricParam.type: indicates the EXCEPTION.
    -   The type of alarm dimension \(dimensions.key\):rpc \(interface name\)
    -   Metrics for requesting such alarm data \(alertRule.rules.measure\):
        -   appstat.exception.rt: response time for API calls due to application exceptions \(milliseconds\)
        -   appstat.exception.count: the number of abnormal API calls

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=SearchAlertRules &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <SearchAlertRulesResponse> <PageBean> <TotalCount> 1 </TotalCount> <PageSize> 10 </PageSize> <PageNumber> 1 </PageNumber> <AlertRules> <Status> RUNNING </Status> <AlertVersion> 1 </AlertVersion> <TaskId> 0 </TaskId> <MetricParam> <Type> TXN </Type> <AppId> 537118 </AppId> <AppGroupId> DEFAULT </AppGroupId> <Dimensions> <Type> ALL </Type> <Value> </Value> <Key> rpc </Key> </Dimensions> <Pid> 9870ca99-8105-4da7-a3a4-d72dd1b1**** </Pid> </MetricParam> <Config> {"continuous":false,"dataRevision":2,"ownerId":"1084900439941126"} </Config> <CreateTime> 1594195623000 </CreateTime> <AlertWays> SMS </AlertWays> <AlertWays> MAIL </AlertWays> <AlertWays> ding_robot </AlertWays> <TaskStatus> </TaskStatus> <AlarmContext> <AlarmContentTemplate> alarm name: $alarm name \n Filters: $screening \n alarm time: $alarm time \n warning: $alarm contents \n note! : The alert is being triggered continuously before a recovery email is received. A notification will be sent to you in 24 hours. </AlarmContentTemplate> <AlarmContentSubTitle> </AlarmContentSubTitle> </AlarmContext> <AlertType> 7 </AlertType> <ContactGroupIdList> 572* </ContactGroupIdList> <Notice> <EndTime> 1480607940000 </EndTime> <NoticeStartTime> 1480521600000 </NoticeStartTime> <StartTime> 1480521600000 </StartTime> <NoticeEndTime> 1480607940000 </NoticeEndTime> </Notice> <UserId> 113197164949**** </UserId> <AlertTitle> TestAlertRule </AlertTitle> <UpdateTime> 1594195623000 </UpdateTime> <AlertLevel> WARN </AlertLevel> <Id> 123 </Id> <RegionId> cn-hangzhou </RegionId> <AlertRule> <Operator> | </Operator> <Rules> <NValue> 5 </NValue> <Operator> current_gte </Operator> <Aggregates> AVG </Aggregates> <Alias> invocation response time_Ms </Alias> <Measure> appstat.transaction.rt </Measure> <Value> 2000 </Value> </Rules> <Rules> <NValue> 5 </NValue> <Operator> current_gte </Operator> <Aggregates> AVG </Aggregates> <Alias> call error number </Alias> <Measure> appstat.transaction.error </Measure> <Value> 1 </Value> </Rules> </AlertRule> </AlertRules> </PageBean> <RequestId> 34ed024e-9e31-434a-9e4e-d9d15c3c**** </RequestId> </SearchAlertRulesResponse> 
   
```

`JSON`

```

     {"PageBean": { "TotalCount": 1, "PageSize": 10, "PageNumber": 1, "AlertRules": [ { "Status": "RUNNING", "AlertVersion": 1, "TaskId": 0, "MetricParam": { "Type": "TXN", "AppId": "537118", "AppGroupId": "DEFAULT", "Dimensions": [ { "Type": "ALL", "Value": "", "Key": "rpc" } ], "Pid": "9870ca99-8105-4da7-a3a4-d72dd1b1****" }, "Config": "{\"continuous\":false,\"dataRevision\":2,\"ownerId\":\"1084900439941126\"}", "CreateTime": 1594195623000, "AlertWays": [ "SMS", "MAIL"," DING_ROBOT " ], " TaskStatus ": " ", " AlarmContext ": { " AlarmContentTemplate ": " Alarm name: $alarm name \nfilter condition: $filter \nalarm Time: $alarm time \nalarm content: $alarm content \nnote! : The alert is being triggered continuously before a recovery email is received. A notification will be sent to you in 24 hours. ", "AlarmContentSubTitle": "" }, "AlertType": 7, "ContactGroupIdList": "572*", "Notice": { "EndTime": 1480607940000, "NoticeStartTime": 1480521600000," StartTime": 1480521600000, "NoticeEndTime": 1480607940000 }, "UserId": "113197164949****", "AlertTitle": "TestAlertRule", "UpdateTime": 1594195623000, "AlertLevel": "WARN", "Id": 123, "RegionId": "cn-hangzhou", "AlertRule": { "Operator": "|", "Rules": [ { " NValue ": 5, " Operator ": " CURRENT_GTE ", " Aggregates ": " AVG ", " Alias ": " Call response time_ms ", " Measure ": " appstat.transaction.rt ", " Value ": 2000 },{" NValue ": 5, " Operator ": " CURRENT_GTE ", " Aggregates ": " AVG ", " Alias ": " number of call errors ", " Measure": "appstat.transaction.error", "Value": 1 } ] } } ] }, "RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3C****"} 
   
```

