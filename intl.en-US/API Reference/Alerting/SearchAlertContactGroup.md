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
|ContactId|Long|No|123|The ID of the alert contact. You can call the SearchAlertContact operation to query the contact IDs. For more information, see [SearchAlertContact](~~130703~~). |
|ContactGroupIds|String|No|746|The ID of the alert contact group. You can query multiple alert contact groups at a time. Separate multiple group IDs with commas \(,\). |
|IsDetail|Boolean|No|true|Specifies whether to return all the alert contacts in the queried alert contact group. Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactGroups|Array of ContactGroup| |The information about the alert contact groups. |
|ContactGroupId|Long|746|The ID of the alert contact group. |
|ContactGroupName|String|TestGroup|The name of the alert contact group. |
|Contacts|Array of Contact| |The information about the alert contacts. |
|ContactId|Long|123|The ID of the alert contact. |
|ContactName|String|John Doe|The name of the alert contact. |
|CreateTime|Long|1572349025000|The timestamp when the alert contact was created. |
|DingRobot|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f6\*\*\*\*|The webhook URL of the DingTalk chatbot. |
|Email|String|someone@example.com|The email address of the alert contact. |
|Phone|String|1381111\*\*\*\*\*|The mobile number of the alert contact. |
|SystemNoc|Boolean|false|Indicates whether the alert contact receives system notifications. Valid values:

 -   true: receives system notifications.
-   false: does not receive system notifications. |
|UpdateTime|Long|1580258717000|The timestamp when the alert contact was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|CreateTime|Long|1529668855000|The timestamp when the alert contact group was created. |
|UpdateTime|Long|1529668855000|The timestamp when the alert contact group was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|RequestId|String|4D6C358A-A58B-4F4B-94CE-F5AAF023\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchAlertContactGroup
&RegionId=cn-hangzhou
&ContactGroupName=TestGroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SearchAlertContactGroupResponse>
  <ContactGroups>
        <ContactGroupId>746</ContactGroupId>
        <UpdateTime>1529668855000</UpdateTime>
        <ContactGroupName>TestGroup</ContactGroupName>
        <UserId>113197164949****</UserId>
        <CreateTime>1529668855000</CreateTime>
  </ContactGroups>
  <ContactGroups>
        <Contacts>
              <Email>someone@example.com</Email>
              <UserId>113197164949****</UserId>
              <Phone>1381111*****</Phone>
              <CreateTime>1572349025000</CreateTime>
              <UpdateTime>1580258717000</UpdateTime>
              <ContactId>123</ContactId>
              <DingRobot>https://oapi.dingtalk.com/robot/send?access_token=91f2f6****</DingRobot>
              <SystemNoc>false</SystemNoc>
              <ContactName>John Doe</ContactName>
        </Contacts>
  </ContactGroups>
  <RequestId>4D6C358A-A58B-4F4B-94CE-F5AAF023****</RequestId>
</SearchAlertContactGroupResponse>
```

`JSON` format

```
{
    "ContactGroups": [
        {
            "ContactGroupId": 746,
            "UpdateTime": 1529668855000,
            "ContactGroupName": "TestGroup",
            "UserId": "113197164949****",
            "CreateTime": 1529668855000
        },
        {
            "Contacts": {
                "Email": "someone@example.com",
                "UserId": "113197164949****",
                "Phone": "1381111*****",
                "CreateTime": 1572349025000,
                "UpdateTime": 1580258717000,
                "ContactId": 123,
                "DingRobot": "https://oapi.dingtalk.com/robot/send?access_token=91f2f6****",
                "SystemNoc": false,
                "ContactName": "John Doe"
            }
        }
    ],
    "RequestId": "4D6C358A-A58B-4F4B-94CE-F5AAF023****"
}
```

