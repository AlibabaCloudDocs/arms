# SearchAlertRules

Queries alert rules.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertRules|The operation that you want to perform. Set the value to `SearchAlertRules`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Title|String|No|AlertRuleTitle|The name of the alert rule. |
|Type|String|No|4|The type of the alert rule. Valid values:

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
|Pid|String|No|atc889zkcf@d8deedfa9bf\*\*\*\*|The process identifier \(PID\) of the application that is associated with the alert rule. For more information, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |
|AppType|String|No|TRACE|The type of the application that is associated with the alert rule. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The struct returned. |
|AlertRules|Array of AlertRuleEntity| |The information about alert rules. |
|AlarmContext|Struct| |The format of the alert notification. |
|AlarmContentSubTitle|String|TestSubTitle|The sub-title of the alert notification content. |
|AlarmContentTemplate|String|Alert name: $alert name\\nFilter condition: $filter\\nAlert time: $alert time\\nAlert content: $alert content\\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.|The template of the alert notification. |
|Content|String|Alert name: $alert name\\nFilter condition: $filter\\nAlert time: $alert time\\nAlert content: $alert content\\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.|The content of the alert notification. |
|SubTitle|String|test|The sub-title of the alert notification. |
|AlertLevel|String|WARN|The severity of the alerts. Only the value `WARN` is supported. |
|AlertRule|Struct| |The conditions of alert rules. Multiple conditions are separated by the AND or OR logical operators. |
|Operator|String|\||The logical operator between conditions. Valid values: `&`: AND. `|`: OR. |
|Rules|Array of Rule| |The condition of the alert rule. |
|Aggregates|String|AVG|The aggregation logic of the alert rule. Valid values:

 -   `AVG`: calculates the average value within minutes.
-   `SUM`: calculates the total value within minutes.
-   `MAX`: calculates the maximum value within minutes.
-   `MIN`: calculates the minimum value within minutes. |
|Alias|String|response time\_ms|The display text of the alert metric. |
|Measure|String|appstat.jvm.SystemDiskFree|The metric based on which alerts are triggered. For more information, see [Alert metrics](https://www.alibabacloud.com/help/zh/doc-detail/175825.htm?spm=a2c63.p38356.b99.373.61d25830rs3HHm#h2-url-4). |
|NValue|Integer|5|The time range to query. Unit: minutes. For example, the value 5 indicates that the alert rule applies to the data in the last 5 minutes. |
|Operator|String|CURRENT\_GTE|The operation logic of the condition. Valid values:

 -   CURRENT\_GTE: greater than or equal to
-   CURRENT\_LTE: less than or equal to
-   PREVIOUS\_UP: the minute-to-minute increase percentage
-   PREVIOUS\_DOWN: the minute-to-minute decrease percentage
-   HOH\_UP: the increase percentage compared with the previous hour
-   HOH\_DOWN: the decrease percentage compared with the previous hour
-   DOD\_UP: the increase percentage compared with the last day
-   DOD\_DOWN: the decrease percentage compared with the last day |
|Value|Float|30|The threshold of the condition. |
|AlertTitle|String|TestAlertRule|The name of the alert rule. |
|AlertType|Integer|4|The type of the alert rule. Valid values:

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|AlertVersion|Integer|1|The version of the alert rule. Default value: `1`. |
|AlertWay|List|null|The notification method of the alerts. Valid values:

 -   `SMS`: text message
-   `MAIL`: email
-   `DING_ROBOT`: DingTalk chatbot |
|AlertWays|List|\["MAIL", "SMS", "DING\_ROBOT"\]|The notification methods of the alerts. Valid values:

 -   `SMS`: text message
-   `MAIL`: email
-   `DING_ROBOT`: DingTalk chatbot |
|Config|String|\{\\"continuous\\":true,\\"dataRevision\\":2\}|The configuration items of the alert rule. The value is a JSON string.

 The configuration item **continuous** specifies whether to continuously send alert notifications. Valid values:

 -   `true`: Send alert notifications every minute.
-   `false`: Enable the alert silence feature.

 The configuration item **dataRevision** specifies the data revision policy to be used if no data is obtained or the data is null. Valid values:

 -   `0`: Overwrite the data by using the value 0.
-   `1`: Overwrite the data by using the value 1.
-   `2`: Overwrite the data by using the value null. This value indicates that no alert is triggered if no data exists. This value is used by default. |
|ContactGroupIdList|String|381\*,572\*|The ID of the contact group. Multiple IDs are separated by commas \(,\). |
|ContactGroupIds|String|\[123, 234\]|The IDs of the alert contact groups. The value is a JSON array. |
|CreateTime|Long|1579508519683|The timestamp when the alert rule was created. |
|Id|Long|123|The ID of the alert rule. |
|MetricParam|Struct| |The information about the application that is associated with the alert rule. |
|AppGroupId|String|DEFAULT|The ID of the application group that is associated with the alert rule. This parameter is applicable to Enterprise Distributed Application Service \(EDAS\) applications. |
|AppId|String|123|The auto-increment ID of the Application Real-Time Monitoring Service \(ARMS\) application. You can ignore this ID. |
|Dimensions|Array of Dimension| |The dimensions in the condition. |
|Key|String|rootIp|The key of the dimension. Valid values:

 -   `rpc`: the name of the API operation
-   `rpcType`: the type of the API call, such as HTTP or Apache Dubbo
-   `endpoint`: the name of the database
-   `rootIp`: the IP address of the host |
|Type|String|DISABLED|The type of the dimension. Valid values:

 -   `STATIC`: checks only the value of this dimension. In this case, you must set the **dimensions.value** parameter.
-   `ALL`: checks the values of all dimensions. The metrics of all API operations are checked. If an operation triggers an alert, the operation name is displayed in the alert notification. In this case, you do not need to set the **dimensions.value** parameter.
-   `DISABLE`: aggregates the values of all dimensions. In this case, you do not need to set the **dimensions.value** parameter. |
|Value|String|"127.0.0.1"|The value of the dimension. |
|Pid|String|9870ca99-8105-4da7-a3a4-d72dd1b1\*\*\*\*|The PID of the application that is associated with the alert rule. |
|Type|String|DB|The type of the metric.

 -   `txn`: the number of API calls during application monitoring
-   `txn_type`: the types of API calls during application monitoring
-   `db`: database metrics
-   `jvm`: Java virtual machine \(JVM\) metrics
-   `host`: host metrics
-   `exception`: API call errors |
|Notice|Struct| |The time ranges when the alert rule takes effect and when alert notifications are sent. |
|EndTime|Long|1480607940000|The end of the time range when the alert rule takes effect within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|NoticeEndTime|Long|1480607940000|The end of the time range when alert notifications are sent based on the alert rule within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|NoticeStartTime|Long|1480521600000|The beginning of the time range when alert notifications are sent based on the alert rule within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|StartTime|Long|1480521600000|The beginning of the time range when the alert rule takes effect within the 24 hours per day. This value is a UNIX timestamp. The year, month, and day that are indicated by the timestamp do not take effect. Only the hour, minute, and second take effect. |
|RegionId|String|cn-hangzhou|The ID of the region to which the alert rule belongs. |
|Status|String|RUNNING|The status of the alert rule. Valid values: `RUNNING`: The alert rule is enabled. `STOPPED`: The alert rule is disabled. |
|TaskId|Long|123|The ID of the ARMS task that is associated with the alert rule. |
|TaskStatus|String|""|The status of the task. It is an internal parameter. |
|Title|String|AlertTest|The title of the alert notification. |
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
        -   appstat.jvm.heap\_used: the total memory space in the JVM heap, in bytes
        -   appstat.jvm.GcPsScavengeCount: the number of garbage collections \(GCs\) in JVM
        -   appstat.jvm.GcPsMarkSweepCount: the number of tag deletions in JVM
        -   appstat.jvm.GcG1OldGenCount: the number of Garbage-First \(G1\) GCs in the old generation
        -   appstat.jvm.GcG1YoungGenCount: the number of G1 GCs in the young generation
        -   appstat.jvm.gc.YoungGcCountInstant: the number of GCs in the young generation
        -   appstat.jvm.gc.OldGcCountInstant: the number of full heap GCs \(Full GCs\) in JVM
        -   appstat.jvm.gc.YoungGcTimeInstant: the time that is consumed for the GCs in the young generation, in milliseconds
        -   appstat.jvm.gc.OldGcTimeInstant: the time that is consumed for the Full GCs in JVM, in milliseconds
        -   appstat.jvm.ThreadCount: the total number of JVM threads
        -   appstat.jvm.non\_heap\_used: the used space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_max: the maximum space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_init: the initial space of the non-heap JVM memory, in bytes
        -   appstat.jvm.non\_heap\_committed: the submitted space of the non-heap JVM memory, in bytes
-   Alert type \(metricParam.type\): HOST
    -   Dimension \(dimensions.key\): rootIp
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.jvm.SystemCpuUser: the used CPU of the host, in percentage
        -   appstat.jvm.SystemMemFree: the idle memory space of the host, in bytes
        -   appstat.jvm.SystemDiskFree: the idle disk space of the host, in bytes
        -   appstat.jvm.SystemNetInErrs: the number of error messages that is received by the host
        -   appstat.jvm.SystemNetOutErrs: the number of error messages that is sent by the host
        -   appstat.jvm.SystemLoad: the system load of the host
-   Alert type \(metricParam.type\): EXCEPTION
    -   Dimension \(dimensions.key\): rpc
    -   Metrics \(alertRule.rules.measure\):
        -   appstat.exception.rt: the response time of abnormal API calls for the application, in milliseconds
        -   appstat.exception.count: the number of abnormal API calls for the application

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchAlertRules
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertRulesResponse>
  <PageBean>
        <TotalCount>23</TotalCount>
        <PageSize>20</PageSize>
        <PageNumber>1</PageNumber>
        <AlertRules>
              <Status>RUNNING</Status>
              <TaskId>123</TaskId>
              <AlertVersion>1</AlertVersion>
              <ContactGroupIds>[123, 234]</ContactGroupIds>
              <Config>{\"continuous\":true,\"dataRevision\":2}</Config>
              <CreateTime>1579508519683</CreateTime>
              <Title>AlertTest</Title>
              <TaskStatus>""</TaskStatus>
              <AlertType>4</AlertType>
              <ContactGroupIdList>381*,572*</ContactGroupIdList>
              <UserId>113197164949****</UserId>
              <UpdateTime>1480521600000</UpdateTime>
              <AlertTitle>TestAlertRule</AlertTitle>
              <AlertLevel>WARN</AlertLevel>
              <RegionId>cn-hangzhou</RegionId>
              <Id>123</Id>
              <AlertWays>["MAIL", "SMS", "DING_ROBOT"]</AlertWays>
              <AlertWay>null</AlertWay>
              <AlarmContext>
                    <AlarmContentTemplate>Alert name: $alert name\nFilter condition: $filter\nAlert time: $alert time\nAlert content: $alert content\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later. </AlarmContentTemplate>
                    <AlarmContentSubTitle>TestSubTitle</AlarmContentSubTitle>
                    <Content>Alert name: $alert name\nFilter condition: $filter\nAlert time: $alert time\nAlert content: $alert content\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later. </Content>
                    <SubTitle>test</SubTitle>
              </AlarmContext>
              <AlertRule>
                    <Operator>|</Operator>
                    <Rules>
                          <Operator>CURRENT_GTE</Operator>
                          <NValue>5</NValue>
                          <Aggregates>AVG</Aggregates>
                          <Alias>response time_ms</Alias>
                          <Value>30</Value>
                          <Measure>appstat.jvm.SystemDiskFree</Measure>
                    </Rules>
              </AlertRule>
              <MetricParam>
                    <Type>DB</Type>
                    <AppId>123</AppId>
                    <AppGroupId>DEFAULT</AppGroupId>
                    <Pid>9870ca99-8105-4da7-a3a4-d72dd1b1****</Pid>
                    <Dimensions>
                          <Type>DISABLED</Type>
                          <Value>"127.0.0.1"</Value>
                          <Key>rootIp</Key>
                    </Dimensions>
              </MetricParam>
              <Notice>
                    <EndTime>1480607940000</EndTime>
                    <NoticeStartTime>1480521600000</NoticeStartTime>
                    <StartTime>1480521600000</StartTime>
                    <NoticeEndTime>1480607940000</NoticeEndTime>
              </Notice>
        </AlertRules>
  </PageBean>
  <RequestId>34ED024E-9E31-434A-9E4E-D9D15C3****</RequestId>
</SearchAlertRulesResponse>
```

`JSON` format

```
{
    "PageBean": {
        "TotalCount": 23,
        "PageSize": 20,
        "PageNumber": 1,
        "AlertRules": {
            "Status": "RUNNING",
            "TaskId": 123,
            "AlertVersion": 1,
            "ContactGroupIds": "[123, 234]",
            "Config": "{\\\"continuous\\\":true,\\\"dataRevision\\\":2}",
            "CreateTime": 1579508519683,
            "Title": "AlertTest",
            "TaskStatus": "\"\"",
            "AlertType": 4,
            "ContactGroupIdList": "381*,572*",
            "UserId": "113197164949****",
            "UpdateTime": 1480521600000,
            "AlertTitle": "TestAlertRule",
            "AlertLevel": "WARN",
            "RegionId": "cn-hangzhou",
            "Id": 123,
            "AlertWays": "[\"MAIL\", \"SMS\", \"DING_ROBOT\"]",
            "AlertWay": "null",
            "AlarmContext": {
                "AlarmContentTemplate": "Alert name: $alert name\\nFilter condition: $filter\\nAlert time: $alert time\\nAlert content: $alert content\\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.",
                "AlarmContentSubTitle": "TestSubTitle",
                "Content": "Alert name: $alert name\\nFilter condition: $filter\\nAlert time: $alert time\\nAlert content: $alert content\\nNote: The alert is continuously triggered until a reply email is received. The system will remind you 24 hours later.",
                "SubTitle": "test"
            },
            "AlertRule": {
                "Operator": "|",
                "Rules": {
                    "Operator": "CURRENT_GTE",
                    "NValue": 5,
                    "Aggregates": "AVG",
                    "Alias": "response time_ms",
                    "Value": 30,
                    "Measure": "appstat.jvm.SystemDiskFree"
                }
            },
            "MetricParam": {
                "Type": "DB",
                "AppId": 123,
                "AppGroupId": "DEFAULT",
                "Pid": "9870ca99-8105-4da7-a3a4-d72dd1b1****",
                "Dimensions": {
                    "Type": "DISABLED",
                    "Value": "\"127.0.0.1\"",
                    "Key": "rootIp"
                }
            },
            "Notice": {
                "EndTime": 1480607940000,
                "NoticeStartTime": 1480521600000,
                "StartTime": 1480521600000,
                "NoticeEndTime": 1480607940000
            }
        }
    },
    "RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3****"
}
```

