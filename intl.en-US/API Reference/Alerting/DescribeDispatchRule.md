# DescribeDispatchRule

Queries the information about a dispatch policy.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DescribeDispatchRule&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDispatchRule|The operation that you want to perform. Set the value to DescribeDispatchRule. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Id|String|No|12345|The ID of the dispatch policy. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DispatchRule|Struct| |The struct returned. |
|GroupRules|Array of GroupRule| |The information about groups. |
|GroupId|Long|1|The ID of the group. |
|GroupInterval|Long|15|The grouping interval. |
|GroupWaitTime|Long|10|The waiting time for grouping. |
|GroupingFields|List|\_aliyun\_arms\_involvedObject\_kind|The grouping fields. |
|LabelMatchExpressionGrid|Struct| |The information about the dispatch rule. |
|LabelMatchExpressionGroups|Array of LabelMatchExpressionGroup| |The collection of dispatch rules. |
|LabelMatchExpressions|Array of LabelMatchExpression| |The collection of conditions of the dispatch rule. |
|Key|String|\_aliyun\_arms\_involvedObject\_kind|The key of the tag of the dispatch rule. Valid values:

 -   `_aliyun_arms_userid`: user ID
-   `_aliyun_arms_involvedObject_kind`: type of the associated object
-   `_aliyun_arms_involvedObject_id`: ID of the associated object
-   `_aliyun_arms_involvedObject_name`: name of the associated object
-   `_aliyun_arms_alert_name`: alert name
-   `_aliyun_arms_alert_rule_id`: alert rule ID
-   `_aliyun_arms_alert_type`: alert type
-   `_aliyun_arms_alert_level`: alert severity |
|Operator|String|eq|The operator used in the dispatch rule. Valid values:

 -   `eq`: equals to.
-   `re`: matches a regular expression. |
|Value|String|app|The value of the tag. |
|Name|String|Prometheus Alert|The name of the dispatch policy. |
|NotifyRules|Array of NotifyRule| |The collection of notification methods. |
|NotifyChannels|List|email|The notification method. Valid values:

 -   `dingTalk`
-   `sms`
-   `webhook`
-   `email`
-   `wechat` |
|NotifyObjects|Array of NotifyObject| |The collection of alert contacts. |
|Name|String|JohnDoe|The name of the contact or contact group. |
|NotifyObjectId|String|1|The ID of the contact or contact group. |
|NotifyType|String|CONTACT|The type of the alert contact. Valid values:

 -   `CONTACT`: contact
-   `CONTACT_GROUP`: contact group |
|RuleId|Long|10282|The ID of the dispatch rule. |
|State|String|true|Indicates whether the dispatch policy is enabled. Valid values:

 -   `true`: enabled
-   `false`: disabled |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DescribeDispatchRule
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDispatchRuleResponse>
  <RequestId>34ED024E-9E31-434A-9E4E-D9D15C3****</RequestId>
  <DispatchRule>
        <GroupRules>
              <GroupInterval>15</GroupInterval>
              <GroupWaitTime>10</GroupWaitTime>
              <GroupId>1</GroupId>
        </GroupRules>
        <GroupRules>
              <GroupingFields>_aliyun_arms_involvedObject_kind</GroupingFields>
        </GroupRules>
        <State>true</State>
        <RuleId>10282</RuleId>
        <LabelMatchExpressionGrid>
              <LabelMatchExpressionGroups>
                    <LabelMatchExpressions>
                          <Operator>eq</Operator>
                          <Value>app</Value>
                          <Key>_aliyun_arms_involvedObject_kind</Key>
                    </LabelMatchExpressions>
              </LabelMatchExpressionGroups>
        </LabelMatchExpressionGrid>
        <NotifyRules>
              <NotifyObjects>
                    <NotifyType>CONTACT</NotifyType>
                    <NotifyObjectId>1</NotifyObjectId>
                    <Name>JohnDoe</Name>
              </NotifyObjects>
        </NotifyRules>
        <NotifyRules>
              <NotifyChannels>email</NotifyChannels>
        </NotifyRules>
        <Name>Prometheus Alert</Name>
  </DispatchRule>
</DescribeDispatchRuleResponse>
```

`JSON` format

```
{
    "RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3****",
    "DispatchRule": {
        "GroupRules": [
            {
                "GroupInterval": 15,
                "GroupWaitTime": 10,
                "GroupId": 1
            },
            {
                "GroupingFields": "_aliyun_arms_involvedObject_kind"
            }
        ],
        "State": true,
        "RuleId": 10282,
        "LabelMatchExpressionGrid": {
            "LabelMatchExpressionGroups": {
                "LabelMatchExpressions": {
                    "Operator": "eq",
                    "Value": "app",
                    "Key": "_aliyun_arms_involvedObject_kind"
                }
            }
        },
        "NotifyRules": [
            {
                "NotifyObjects": {
                    "NotifyType": "CONTACT",
                    "NotifyObjectId": 1,
                    "Name": "JohnDoe"
                }
            },
            {
                "NotifyChannels": "email"
            }
        ],
        "Name": "Prometheus Alert"
    }
}
```

