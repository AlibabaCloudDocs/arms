# SearchAlertHistories

Call SearchAlertHistories interface query alarm rules in the actions of the alarm transmission records.

**** ****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=SearchAlertHistories&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertHistories|The parameter specified by the system. Valid values: `SearchAlertHistories` . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. The default is `cn-hangzhou` . |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |
|AlertId|Long|No|123|The ID of the alarm rule. You can call the SearchAlertRules operation to query the `Id` \), please refer to [SearchAlertRules](~~175825~~) . |
|AlertType|Integer|No|4|The type of the alarm rule. Valid values:

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus alert rule |
|CurrentPage|Integer|No|1|The number of the page to return. The default is `1` . |
|PageSize|Integer|No|10|The number of items displayed on each page. The default is `10` . |
|StartTime|Long|No|1595568910000|The timestamp used to query the start time of historical alarm records. The format is Unix Timestamp Long, in milliseconds. The default value is 10 minutes before the current time. |
|EndTime|Long|No|1579499626000|The timestamp of the end time of the query. The format is Unix Timestamp Long, in milliseconds. The time to test rules. The default value is the current time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The returned data struct. |
|AlarmHistories|Array| |The list of historical alarm objects. |
|AlarmContent|String|"Alarm name: Alert1 \\nalarm Time: 2020-07-24 12:14:00 \\nalarm content: a total of 4 records triggering exception: \*\*\*"|Alarm Detail |
|AlarmResponseCode|Integer|200|Status Code returned by alarm logshipper |
|AlarmSources|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca\*\*\*\*|Alarm Webhook \(such as DingTalk the Webhook address of the robot\) |
|AlarmTime|Long|1595564179000|Alarm sending time |
|AlarmType|Integer|4|Alarm rule type \(default value: 4\):

 -   `1` : Custom monitoring alarm rule based on the drill-down dataset.
-   `3` : Custom monitoring alarm rule based on tiled dataset.
-   `4` : browser monitoring alarm rules, including the default browser monitoring alarm rules \(AlertType=6\).
-   `5` : application monitoring alert rule, including application monitoring default alert rule \(AlertType=7\).
-   `6` : default browser monitoring alarm rule
-   `7` : The alert rule is application monitoring by default.
-   `8` : Tracing Analysis alert rule
-   `101` : Prometheus monitoring alarm rules. |
|Emails|String|someone@example.com|The email address of the alert recipient. |
|Id|Long|123|The ID of the alert notification to send. |
|Phones|String|1381111\*\*\*\*|The mobile phone number that receives the alert. |
|StrategyId|String|""|Internal field |
|Target|String|""|Internal field |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|PageNumber|Integer|1|The number of the page to return. |
|PageSize|Integer|10|The number of projects that are displayed on each page. |
|TotalCount|Integer|2|The total number of entries returned. |
|RequestId|String|2FC13182-B9AF-4E6B-BE51-72669B7C\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=SearchAlertHistories &RegionId=cn-hangzhou &AlertId=123 &StartTime=1579499026000 &EndTime=1579499626000 &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <SearchAlertHistoriesResponse> <PageBean> <TotalCount> 2 </TotalCount> <PageSize> 10 </PageSize> <PageNumber> 1 </PageNumber> <AlarmHistories> <Target> </Target> <Phones> 1381111 **** </Phones> <AlarmTime> 1595564179000 </AlarmTime> <UserId> 113197164949 **** </UserId> <AlarmType> 4 </AlarmType> <AlarmResponseCode> 200 </AlarmResponseCode> <StrategyId> </StrategyId> <Id> 123 </Id> <AlarmContent> alarm name: Alert1 alarm Time: 2020-07-24 12:14:00 alarm contents: a total of 4 records trigger an exception: **** </AlarmContent> <Emails> someone1@example.com </Emails> <AlarmSources> https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca **** </AlarmSources> </AlarmHistories> <AlarmHistories> <Target> </Target> <Phones> 1381111 **** </Phones> <AlarmTime> 1595564038000 </AlarmTime> <UserId> 113197164949 **** </UserId> <AlarmType> 4 </AlarmType> <AlarmResponseCode> 200 </AlarmResponseCode> <StrategyId> </StrategyId> <Id> 321 </Id> <AlarmContent> alarm name: Alert1 alarm Time: 2020-07-24 12:14:00 alarm content: a total of 4 records triggering exception: **** </AlarmContent> <Emails> someone2@example.com </Emails> <AlarmSources> https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca **** </AlarmSources> </AlarmHistories> </PageBean> <RequestId> 2FC13182-B9 AF-4E6B-BE51-72669B7C **** </RequestId> </SearchAlertHistoriesResponse> 
   
```

`JSON`

```

     {"PageBean": { "TotalCount": 2, "PageSize": 10, "PageNumber": 1, "AlarmHistories": [ { "Target": "", "Phones": "1381111****", "AlarmTime": 1595564179000, "UserId": "113197164949****", "AlarmType": 4, "AlarmResponseCode": 200," StrategyId ": " ", " Id ": 123, " AlarmContent ": " Alarm name: Alert1\n alarm Time: 2020-07-24 12:14:00\n alarm content: a total of 4 records are triggered: Exception * ", " Emails ": " someone1@example.com ", " AlarmSources ": " https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca ###* "}, { " Target ": " ", " Phones ": " 1381111 ###* ", " AlarmTime ": 1595564038000," UserId ": " 113197164949 ###* ", " AlarmType ": 4, " AlarmResponseCode ": 200," StrategyId": ", " Id ": " 321, "AlarmContent": "Alarm name: Alert1 \nalarm Time: 2020-07-24, 12:14:00 \nalarm content: a total of 4 records are triggered: exception triggered *", "Emails": "someone2@example.com", "AlarmSources":" https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca ****" } ] }, "RequestId": "2FC13182-B9AF-4E6B-BE51-72669B7C****"} 
   
```

