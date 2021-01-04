# SearchAlertHistories

Queries alert records of an alert rule.

********

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertHistories&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertHistories|The operation that you want to perform. Set the value to `SearchAlertHistories`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Set the value to `cn-hangzhou`. |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |
|AlertId|Long|No|123|The ID of the alert rule. You can call the SearchAlertRules operation and view the `Id` parameter in the response. For more information, see [SearchAlertRules](~~175825~~). |
|AlertType|Integer|No|4|The type of the alert rule.

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|CurrentPage|Integer|No|1|The number of the page to return. Default value: `1`. |
|PageSize|Integer|No|10|The number of entries to return on each page. Default value: `10`. |
|StartTime|Long|No|1595568910000|The beginning of the time range to query. This value is a UNIX Timestamp of the LONG data type, in milliseconds. The default value is 10 minutes before the current time. |
|EndTime|Long|No|1579499626000|The end of the time range to query. This value is a UNIX Timestamp of the LONG data type, in milliseconds. The default value is the current time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The returned data structure. |
|AlarmHistories|Array| |The list of alert records. |
|AlarmContent|String|"Alert name: Alert1\\nAlert time: 2020-07-24 12:14:00\\nAlert content: A total of 4 alerts are triggered: \*\*\*"|The alert content. |
|AlarmResponseCode|Integer|200|The response code after the alert notification was sent. |
|AlarmSources|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca\*\*\*\*|The webhook URL of the alert contact, such as a DingTalk bot. |
|AlarmTime|Long|1595564179000|The time when the alert notification was sent. |
|AlarmType|Integer|4|The type of the alert rule. Default value: 4. Valid values:

 -   `1`: custom alert rules to monitor drill-down data sets
-   `3`: custom alert rules to monitor tiled data sets
-   `4`: alert rules to monitor the frontend, including the default frontend alert rules
-   `5`: alert rules to monitor applications, including the default application alert rules
-   `6`: the default frontend alert rules
-   `7`: the default application alert rules
-   `8`: Tracing Analysis alert rules
-   `101`: Prometheus alert rules |
|Emails|String|someone@example.com|The email address of the alert contact. |
|Id|Long|123|The ID of the alert notification. |
|Phones|String|1381111\*\*\*\*|The mobile phone number of the alert contact. |
|StrategyId|String|""|The internal field. |
|Target|String|""|The internal field. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|2|The total number of entries returned. |
|RequestId|String|2FC13182-B9AF-4E6B-BE51-72669B7C\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchAlertHistories
&RegionId=cn-hangzhou
&AlertId=123
&StartTime=1579499026000
&EndTime=1579499626000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertHistoriesResponse>
	    <PageBean>
		        <TotalCount>2</TotalCount>
		        <PageSize>10</PageSize>
		        <PageNumber>1</PageNumber>
		        <AlarmHistories>
			            <Target></Target>
			            <Phones>1381111****</Phones>
			            <AlarmTime>1595564179000</AlarmTime>
			            <UserId>113197164949****</UserId>
			            <AlarmType>4</AlarmType>
			            <AlarmResponseCode>200</AlarmResponseCode>
			            <StrategyId></StrategyId>
			            <Id>123</Id>
			            <AlarmContent>Alert name: Alert1
	Alert time: 2020-07-24 12:14:00
	Alert content: A total of 4 alerts are triggered:****</AlarmContent>
			            <Emails>someone1@example.com</Emails>
			            <AlarmSources>https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****</AlarmSources>
		        </AlarmHistories>
		        <AlarmHistories>
			            <Target></Target>
			            <Phones>1381111****</Phones>
			            <AlarmTime>1595564038000</AlarmTime>
			            <UserId>113197164949****</UserId>
			            <AlarmType>4</AlarmType>
			            <AlarmResponseCode>200</AlarmResponseCode>
			            <StrategyId></StrategyId>
			            <Id>321</Id>
			            <AlarmContent>Alert name: Alert1
	Alert time: 2020-07-24 12:14:00
	Alert content: A total of 4 alerts are triggered:****</AlarmContent>
			            <Emails>someone2@example.com</Emails>
			            <AlarmSources>https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****</AlarmSources>
		        </AlarmHistories>
	    </PageBean>
	    <RequestId>2FC13182-B9AF-4E6B-BE51-72669B7C****</RequestId>
</SearchAlertHistoriesResponse>
```

`JSON` format

```
{
	"PageBean": {
		"TotalCount": 2,
		"PageSize": 10,
		"PageNumber": 1,
		"AlarmHistories": [
			{
				"Target": "",
				"Phones": "1381111****",
				"AlarmTime": 1595564179000,
				"UserId": "113197164949****",
				"AlarmType": 4,
				"AlarmResponseCode": 200,
				"StrategyId": "",
				"Id": 123,
				"AlarmContent": "Alert name: Alert1\nAlert time: 2020-07-24 12:14:00\nAlert content: A total of 4 alerts are triggered: ***",
				"Emails": "someone1@example.com",
				"AlarmSources": "https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****"
			},
			{
				"Target": "",
				"Phones": "1381111****",
				"AlarmTime": 1595564038000,
				"UserId": "113197164949****",
				"AlarmType": 4,
				"AlarmResponseCode": 200,
				"StrategyId": "",
				"Id": 321,
				"AlarmContent": "Alert name: Alert1\nAlert time: 2020-07-24 12:14:00\nAlert content: A total of 4 alerts are triggered: ***",
				"Emails": "someone2@example.com",
				"AlarmSources": "https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****"
			}
		]
	},
	"RequestId": "2FC13182-B9AF-4E6B-BE51-72669B7C****"
}
```

