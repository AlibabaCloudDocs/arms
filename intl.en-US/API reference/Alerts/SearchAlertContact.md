# SearchAlertContact

Queries alert contacts.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertContact|The operation that you want to perform. Set the value to `SearchAlertContact`. |
|ContactName|String|Yes|John Doe|The name of the alert contact. |
|CurrentPage|String|Yes|1|The number of the page to return. |
|Email|String|Yes|someone@example.com|The email address of the alert contact. |
|PageSize|String|Yes|20|The number of entries to return on each page. |
|Phone|String|Yes|1381111\*\*\*\*\*|The phone number of the alert contact. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. Default value: `cn-hangzhou`. |
|ProxyUserId|String|No|1234123\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The returned struct. |
|Contacts|Array| |The list of the alert contacts. |
|ContactId|Long|123|The ID of the alert contact. |
|ContactName|String|John Doe|The name of the alert contact. |
|CreateTime|Long|1572349025000|The timestamp when the instance was created. |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|The webhook URL of the DingTalk chatbot. |
|Email|String|someone@example.com|The email address of the alert contact. |
|Phone|String|1381111\*\*\*\*\*|The phone number of the alert contact. |
|SystemNoc|Boolean|false|Indicates whether the system notifications were received. Valid values:

 -   `true`: The system notifications were received.
-   `false`: The system notifications were not received. |
|UpdateTime|Long|1580258717000|The timestamp when the instance was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|TotalCount|Integer|23|The total number of entries that was returned. |
|RequestId|String|21E85B16-75A6-429A-9F65-8AAC9A54\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=SearchAlertContact
&ContactName=John Doe
&CurrentPage=1
&Email=someone@example.com
&PageSize=20
&Phone=1381111*****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertContactResponse>
	  <PageBean>
		    <TotalCount>2</TotalCount>
		    <PageSize>10</PageSize>
		    <Contacts>
			      <Email>someone1@example.com</Email>
			      <UserId>113197164949****</UserId>
			      <Phone>1381111*****</Phone>
			      <CreateTime>1572349025000</CreateTime>
			      <UpdateTime>1580258717000</UpdateTime>
			      <ContactId>123</ContactId>
			      <DingRobot>https://oapi.dingtalk.com/robot/send?access_token=91f2f6****</DingRobot>
			      <ContactName>John Doe</ContactName>
			      <SystemNoc>true</SystemNoc>
		    </Contacts>
		    <Contacts>
			      <Email>someone2@example.com</Email>
			      <Phone>1381111*****</Phone>
			      <UserId>113197164949****</UserId>
			      <CreateTime>1595319998000</CreateTime>
			      <UpdateTime>1595319998000</UpdateTime>
			      <ContactId>456</ContactId>
			      <DingRobot></DingRobot>
			      <ContactName>Jane Doe</ContactName>
			      <SystemNoc>false</SystemNoc>
		    </Contacts>
		    <PageNumber>1</PageNumber>
	  </PageBean>
	  <RequestId>21E85B16-75A6-429A-9F65-8AAC9A54****</RequestId>
</SearchAlertContactResponse>
```

`JSON` format

```
{
	"PageBean": {
		"TotalCount": 2,
		"PageSize": 10,
		"Contacts": [
			{
				"Email": "someone1@example.com",
				"UserId": "113197164949****",
				"Phone": "1381111*****",
				"CreateTime": 1572349025000,
				"UpdateTime": 1580258717000,
				"ContactId": 123,
				"DingRobot": "https://oapi.dingtalk.com/robot/send?access_token=91f2f6****",
				"ContactName": "John Doe",
				"SystemNoc": true
			},
			{
				"Email": "someone2@example.com",
				"Phone": "1381111*****",
				"UserId": "113197164949****",
				"CreateTime": 1595319998000,
				"UpdateTime": 1595319998000,
				"ContactId": 456,
				"DingRobot": "",
				"ContactName": "Jane Doe",
				"SystemNoc": false
			}
		],
		"PageNumber": 1
	},
	"RequestId": "21E85B16-75A6-429A-9F65-8AAC9A54****"
}
```

