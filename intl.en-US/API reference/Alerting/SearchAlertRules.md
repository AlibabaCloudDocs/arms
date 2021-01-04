# SearchAlertRules

Queries alert rules.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertRules|The operation that you want to perform. Set the value to `SearchAlertRules` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |
|Title|String|No|AlertRuleTitle|The name of the alert rule. |
|Type|String|No|4|The type of the alert rule.

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|CurrentPage|Integer|No|1|The number of the page to return. Default value: `1`. |
|PageSize|Integer|No|20|The number of entries to return on each page. Default value: `10`. |
|Pid|String|No|atc889zkcf@d8deedfa9bf\*\*\*\*|The ID of the ARMS application that is associated with the alert rule. Valid types:

 -   the ID of the application that is associated with an application alert rule
-   the ID of a frontend website that is associated with a frontend alert rule |
|AppType|String|No|TRACE|The application type of the alert rule. Valid values:

 -   `TRACE`: monitors applications
-   `RETCODE` : monitors the frontend |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The data structure returned. |
|AlertRules|Array| |The information about alert rules. |
|AlarmContext|Struct| |The format of the alert message. |
|AlarmContentSubTitle|String|TestSubTitle|The sub-title of the alert message. |
|AlarmContentTemplate|String|Alert name: $alert name\\nFiltering condition: $filter\\n Alert time: $alert time\\nAlert content: $alert content\\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.|The template of the alert message. |
|AlertLevel|String|WARN|The level of the alert. Only the value `WARN` is supported. |
|AlertRule|Struct| |The conditions of the alert rule. Multiple conditions are separated with the AND or OR logical operators. |
|Operator|String|\||The logical operator between alert rules. `&`: AND. `|`: OR. |
|Rules|Array| |The conditions of the alert rule. |
|Aggregates|String|AVG|The aggregation logic of alert rules. Valid values:

 -   `AVG`: calculates the average value within minutes
-   `SUM`: calculates the total value within minutes
-   `MAX`: calculates the maximum value within minutes
-   `MIN`: calculates the minimum value within minutes |
|Alias|String|response time\_ms|The display text of the alert metric. |
|Measure|String|appstat.jvm.SystemDiskFree|The metrics based on which alerts are triggered. For more information, see **Alert metrics**. |
|NValue|Integer|5|The time range to query. Unit: minutes. For example, the value 5 indicates that the alert rule applies to the data in the last 5 minutes. |
|Operator|String|CURRENT\_GTE|The operation logic of the condition. Valid values:

 -   CURRENT\_GTE: greater than or equal to
-   CURRENT\_LTE: less than or equal to
-   PREVIOUS\_UP: the minute-to-minute increase percentage
-   PREVIOUS\_DOWN: the minute-to-minute decrease percentage
-   HOH\_UP: the increase percentage compared with the previous hour
-   HOH\_DOWN: the decrease percentage compared with the previous hour
-   DOD\_UP: the increase percentage compared with the last day
-   DOD\_DOWN: the increase percentage compared with the last day |
|Value|Float|30|The threshold of the condition. |
|AlertTitle|String|TestAlertRule|The name of the alert rule. |
|AlertType|Integer|4|The type of the alert rule.

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|AlertVersion|Integer|1|The version of the alert rule. Default value: `1`. |
|AlertWays|List|\["MAIL", "SMS", "DING\_ROBOT"\]|The notification method of the alert. Valid values:

 -   `SMS`: text message
-   `MAIL`: email
-   `DING_ROBOT`: DingTalk bot |
|Config|String|\{\\"continuous\\":true,\\"dataRevision\\":2\}|The configuration items of the alert rule. The value is a JSON string.

 Valid values of **continuous**:

 -   `true`: sends alert notifications every minute
-   `false`: enables the alert silence feature

 **dataRevision** specifies the data revision policy if no data is obtained or data is null. Valid values:

 -   `0`: overwrites by using the value 0.
-   `1`: overwrites by using the value 1.
-   `2`: overwrites by using the value null. This value indicates that no alert is triggered if no data exists. This value is used by default. |
|ContactGroupIdList|String|381\*,572\*|The ID of the contact group. Multiple IDs are separated with commas \(,\). |
|CreateTime|Long|1579508519683|The timestamp when the alert rule was created. |
|Id|Long|123|The ID of the alert rule. |
|MetricParam|Struct| |The information about the application that is associated with the alert rule. |
|AppGroupId|String|DEFAULT|The ID of the application group that is associated with the alert rule. This parameter is applicable to EDAS applications. |
|AppId|String|123|The auto-increment ID of the ARMS application. You can ignore this ID. |
|Dimensions|Array| |The dimensions in the condition. |
|Key|String|rootIp|The name of the dimension. Valid values:

 -   `rpc`: the name of the API operation
-   `rpcType`: the type of the API call, such as HTTP or DUBBO
-   `endpoint`: the name of the database
-   `rootIp`: the IP address of the machine |
|Type|String|DISABLED|The type of the dimension. Valid values:

 -   `STATIC`: only checks the value of this dimension. In this case, you must set the **dimensions.value** parameter.
-   `ALL`: checks the values of all dimensions. The metrics of all API operations are checked. If an operation triggers an alert, the operation name is displayed in the alert message. In this case, you do not need to set the **dimensions.value** parameter.
-   `DISABLE`: aggregates the values of all dimensions. In this case, you do not need to set the **dimensions.value** parameter. |
|Value|String|"127.0.0.1"|The value of the dimension. |
|Pid|String|9870ca99-8105-4da7-a3a4-d72dd1b1\*\*\*\*|The ID of the application that is associated with the alert rule. |
|Type|String|DB|The type of the metric.

 -   `TXN`: the number of API calls during application monitoring
-   `TXN_TYPE`: the types of API calls during application monitoring
-   `DB`: database metrics
-   `JVM`: JVM metrics
-   `HOST`: host metrics
-   `EXCEPTION`: API call errors |
|Notice|Struct| |The time ranges when the alert rule takes effect and when the alert notification is sent. |
|EndTime|Long|1480607940000|The end of the time range when the alert rule takes effect within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|NoticeEndTime|Long|1480607940000|The end of the time range when the alert rule is sent within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|NoticeStartTime|Long|1480521600000|The beginning of the time range when the alert rule is sent within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|StartTime|Long|1480521600000|The beginning of the time range when the alert rule takes effect within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|RegionId|String|cn-hangzhou|The ID of the region to which the alert rule belongs. |
|Status|String|RUNNING|The status of the alert rule. `RUNNING`: The alert rule is running. `STOPPED`: The alert rule is stopped. |
|TaskId|Long|123|The ID of the ARMS task that is associated with the custom alert rule. |
|TaskStatus|String|""|The internal field. |
|UpdateTime|Long|1480521600000|The timestamp when the alert rule was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user to which the alert rule belongs. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|20|The number of entries returned per page. |
|TotalCount|Integer|23|The total number of entries returned. |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|The ID of the request. |

## Alert metrics

-   Alert type \(metricParam.type\): TXN
    -   Dimension \(dimensions.key\): rpc
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.txn.rt: the response time of API calls in milliseconds
        -   appstat.txn.count: the number of API calls
        -   appstat.txn.errcount: the number of API call errors
-   Alert type \(metricParam.type\): TXN\_TYPE
    -   Dimension \(dimensions.key\): rpcType
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.inbound.rt: the response time of API calls for the services that are provided by the application, in milliseconds
        -   appstat.inbound.count: the number of API calls for the services that are provided by the application
        -   appstat.inbound.error: the number of API call errors for the services that are provided by the application
        -   appstat.outbound.rt: the response time of API calls for the services on which the application depends, in milliseconds
        -   appstat.outbound.count: the number of API calls for the services on which the application depends
        -   appstat.outbound.error: the number of API call errors for the services on which the application depends
-   Alert type \(metricParam.type\): DB
    -   Dimension \(dimensions.key\): endpoint
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.database.rt: the response time of API calls for the database
        -   appstat.database.count: the number of API calls for the database
        -   appstat.database.errcount: the number of API call errors for the database
-   Alert type \(metricParam.type\): JVM
    -   Dimension \(dimensions.key\): rootIp
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.jvm.heap\_used: the total memory in the JVM heap, in bytes
        -   appstat.jvm.GcPsScavengeCount: the number of garbage collection \(GC\) in JVM
        -   appstat.jvm.GcPsMarkSweepCount: the number of tag deletions in JVM
        -   appstat.jvm.GcG1OldGenCount: the number of G1GC in JVM\_Old
        -   appstat.jvm.GcG1YoungGenCount: the number of G1GC in JVM\_Young
        -   appstat.jvm.gc.YoungGcCountInstant: the number of GC in JVM\_Young
        -   appstat.jvm.gc.OldGcCountInstant: the number of GC in JVM\_Full
        -   appstat.jvm.gc.YoungGcTimeInstant: the time that takes for the JVM\_Young GC, in milliseconds
        -   appstat.jvm.gc.OldGcTimeInstant: the time that takes for the JVM\_Full GC, in milliseconds
        -   appstat.jvm.ThreadCount: the total number of JVM threads
        -   appstat.jvm.non\_heap\_used: the used space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_max: the total space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_init: the initial space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_committed: the submitted space of the non-heap JVM memory, in bytes
-   Alert type \(metricParam.type\): HOST
    -   Dimension \(dimensions.key\): rootIp
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.jvm.SystemCpuUser: the used CPU of the machine, in percentage
        -   appstat.jvm.SystemMemFree: the idle memory of the machine, in bytes
        -   appstat.jvm.SystemDiskFree: the idle disk space of the machine, in bytes
        -   appstat.jvm.SystemNetInErrs: the number of error messages that is received by the machine
        -   appstat.jvm.SystemNetOutErrs: the number of error messages that is sent by the machine
        -   appstat.jvm.SystemLoad: the system load of the machine
-   Alert type \(metricParam.type\): EXCEPTION
    -   Dimension \(dimensions.key\): rpc
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.exception.rt: the response time of abnormal API calls for the application, in milliseconds
        -   appstat.exception.count: the number of abnormal API calls

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchAlertRules
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertRulesResponse>
	  <PageBean>
		    <TotalCount>1</TotalCount>
		    <PageSize>10</PageSize>
		    <PageNumber>1</PageNumber>
		    <AlertRules>
			      <Status>RUNNING</Status>
			      <AlertVersion>1</AlertVersion>
			      <TaskId>0</TaskId>
			      <MetricParam>
				        <Type>TXN</Type>
				        <AppId>537118</AppId>
				        <AppGroupId>DEFAULT</AppGroupId>
				        <Dimensions>
					          <Type>ALL</Type>
					          <Value></Value>
					          <Key>rpc</Key>
				        </Dimensions>
				        <Pid>9870ca99-8105-4da7-a3a4-d72dd1b1****</Pid>
			      </MetricParam>
			      <Config>{"continuous":false,"dataRevision":2,"ownerId":"1084900439941126"}</Config>
			      <CreateTime>1594195623000</CreateTime>
			      <AlertWays>SMS</AlertWays>
			      <AlertWays>MAIL</AlertWays>
			      <AlertWays>DING_ROBOT</AlertWays>
			      <TaskStatus></TaskStatus>
			      <AlarmContext>
				        <AlarmContentTemplate>Alert name: $alert name\nFiltering condition: $filter\n Alert time: $alert time\nAlert content: $alert content\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later. </AlarmContentTemplate>
				        <AlarmContentSubTitle></AlarmContentSubTitle>
			      </AlarmContext>
			      <AlertType>7</AlertType>
			      <ContactGroupIdList>572*</ContactGroupIdList>
			      <Notice>
				        <EndTime>1480607940000</EndTime>
				        <NoticeStartTime>1480521600000</NoticeStartTime>
				        <StartTime>1480521600000</StartTime>
				        <NoticeEndTime>1480607940000</NoticeEndTime>
			      </Notice>
			      <UserId>113197164949****</UserId>
			      <AlertTitle>TestAlertRule</AlertTitle>
			      <UpdateTime>1594195623000</UpdateTime>
			      <AlertLevel>WARN</AlertLevel>
			      <Id>123</Id>
			      <RegionId>cn-hangzhou</RegionId>
			      <AlertRule>
				        <Operator>|</Operator>
				        <Rules>
					          <NValue>5</NValue>
					          <Operator>CURRENT_GTE</Operator>
					          <Aggregates>AVG</Aggregates>
					          <Alias>response time_ms</Alias>
					          <Measure>appstat.transaction.rt</Measure>
					          <Value>2000</Value>
				        </Rules>
				        <Rules>
					          <NValue>5</NValue>
					          <Operator>CURRENT_GTE</Operator>
					          <Aggregates>AVG</Aggregates>
					          <Alias>the number of API call errors</Alias>
					          <Measure>appstat.transaction.error</Measure>
					          <Value>1</Value>
				        </Rules>
			      </AlertRule>
		    </AlertRules>
	  </PageBean>
	  <RequestId>34ED024E-9E31-434A-9E4E-D9D15C3C****</RequestId>
</SearchAlertRulesResponse>
```

`JSON` format

```
{
	"PageBean": {
		"TotalCount": 1,
		"PageSize": 10,
		"PageNumber": 1,
		"AlertRules": [
			{
				"Status": "RUNNING",
				"AlertVersion": 1,
				"TaskId": 0,
				"MetricParam": {
					"Type": "TXN",
					"AppId": "537118",
					"AppGroupId": "DEFAULT",
					"Dimensions": [
						{
							"Type": "ALL",
							"Value": "",
							"Key": "rpc"
						}
					],
					"Pid": "9870ca99-8105-4da7-a3a4-d72dd1b1****"
				},
				"Config": "{\"continuous\":false,\"dataRevision\":2,\"ownerId\":\"1084900439941126\"}",
				"CreateTime": 1594195623000,
				"AlertWays": [
					"SMS",
					"MAIL",
					"DING_ROBOT"
				],
				"TaskStatus": "",
				"AlarmContext": {
					"AlarmContentTemplate": "Alert name: $alert name\nFiltering condition: $filter\n Alert time: $alert time\nAlert content: $alert content\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.",
					"AlarmContentSubTitle": ""
				},
				"AlertType": 7,
				"ContactGroupIdList": "572*",
				"Notice": {
					"EndTime": 1480607940000,
					"NoticeStartTime": 1480521600000,
					"StartTime": 1480521600000,
					"NoticeEndTime": 1480607940000
				},
				"UserId": "113197164949****",
				"AlertTitle": "TestAlertRule",
				"UpdateTime": 1594195623000,
				"AlertLevel": "WARN",
				"Id": 123,
				"RegionId": "cn-hangzhou",
				"AlertRule": {
					"Operator": "|",
					"Rules": [
						{
							"NValue": 5,
							"Operator": "CURRENT_GTE",
							"Aggregates": "AVG",
							"Alias": "response time_ms",
							"Measure": "appstat.transaction.rt",
							"Value": 2000
						},
						{
							"NValue": 5,
							"Operator": "CURRENT_GTE",
							"Aggregates": "AVG",
							"Alias": "the number of API call errors",
							"Measure": "appstat.transaction.error",
							"Value": 1
						}
					]
				}
			}
		]
	},
	"RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3C****"
}
```

