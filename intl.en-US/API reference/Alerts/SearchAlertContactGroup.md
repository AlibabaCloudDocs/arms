# SearchAlertContactGroup

Queries alert contact groups.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertContactGroup|The operation that you want to perform. Set the value to `SearchAlertContactGroup`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Default value: `cn-hangzhou`. |
|ContactGroupName|String|No|TestGroup|The name of the alert contact group. |
|ContactName|String|No|John Doe|The name of the alert contact. |
|ContactId|Long|No|123|The ID of the alert contact. You can call the SearchAlertContact operation to query the alert contact ID. For more information, see [SearchAlertContact](~~130703~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactGroups|Array of ContactGroup| |The list of alert contact groups. |
|ContactGroupId|Long|746|The ID of the alert contact group. |
|ContactGroupName|String|TestGroup|The name of the alert contact group. |
|Contacts|Array of Contact| |The list of alert contacts. |
|ContactId|Long|123|The ID of the alert contact. |
|ContactName|String|John Doe|The name of the alert contact. |
|CreateTime|Long|1572349025000|The timestamp when the alert contact group was created. |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|The webhook URL of DingTalk chatbot. |
|Email|String|someone@example.com|The email address of the alert contact. |
|Phone|String|1381111\*\*\*\*\*|The phone number of the alert contact. |
|SystemNoc|Boolean|false|Specifies whether to receive system notifications. Valid values:

 -   true: System notifications are received.
-   false: System notifications are not received. |
|UpdateTime|Long|1580258717000|The timestamp when the alert contact group was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|CreateTime|Long|1529668855000|The timestamp when the alert contact group was created. |
|UpdateTime|Long|1529668855000|The timestamp when the alert contact group was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|RequestId|String|4D6C358A-A58B-4F4B-94CE-F5AAF023\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchAlertContactGroup

```

正常返回示例

`XML` 格式

```
<SearchAlertContactGroupResponse> 	  <ContactGroups> 		    <ContactGroupId>746</ContactGroupId> 		    <ContactGroupName>TestGroup</ContactGroupName> 		    <UserId>113197164949****</UserId> 		    <CreateTime>1529668855000</CreateTime> 		    <UpdateTime>1529668855000</UpdateTime> 	  </ContactGroups> 	  <ContactGroups> 		    <ContactGroupId>747</ContactGroupId> 		    <ContactGroupName>TestGroup2</ContactGroupName> 		    <UserId>113197164949****</UserId> 		    <CreateTime>1595383179000</CreateTime> 		    <UpdateTime>1595383179000</UpdateTime> 	  </ContactGroups> 	  <RequestId>4D6C358A-A58B-4F4B-94CE-F5AAF023****</RequestId> </SearchAlertContactGroupResponse>
```

`JSON` 格式

```
{ 	"ContactGroups": [ 		{ 			"ContactGroupId": 746, 			"ContactGroupName": "TestGroup", 			"UserId": "113197164949****", 			"CreateTime": 1529668855000, 			"UpdateTime": 1529668855000 		}, 		{ 			"ContactGroupId": 747, 			"ContactGroupName": "TestGroup2", 			"UserId": "113197164949****", 			"CreateTime": 1595383179000, 			"UpdateTime": 1595383179000 		} 	], 	"RequestId": "4D6C358A-A58B-4F4B-94CE-F5AAF023****" }
```

