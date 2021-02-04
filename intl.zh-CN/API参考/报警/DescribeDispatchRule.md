# DescribeDispatchRule

调用DescribeDispatchRule接口查询分派策略信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DescribeDispatchRule&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDispatchRule|系统规定参数。取值：DescribeDispatchRule。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Id|String|否|12345|分派策略ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DispatchRule|Struct| |返回结构体。 |
|GroupRules|Array of GroupRule| |事件分组。 |
|GroupId|Long|1|分组ID。 |
|GroupInterval|Long|15|分组间隔时间。 |
|GroupWaitTime|Long|10|分组等待时间。 |
|GroupingFields|List|\_aliyun\_arms\_involvedObject\_kind|分组字段列表。 |
|LabelMatchExpressionGrid|Struct| |分派规则。 |
|LabelMatchExpressionGroups|Array of LabelMatchExpressionGroup| |分派条件集合。 |
|LabelMatchExpressions|Array of LabelMatchExpression| |分派规则的条件。 |
|Key|String|\_aliyun\_arms\_involvedObject\_kind|分派条件标签：

 -   `_aliyun_arms_userid` : 用户ID
-   `_aliyun_arms_involvedObject_kind`: 关联对象类型
-   `_aliyun_arms_involvedObject_id`: 关联对象ID
-   `_aliyun_arms_involvedObject_name`: 关联对象名称
-   `_aliyun_arms_alert_name`: 告警名称
-   `_aliyun_arms_alert_rule_id`: 告警规则对应的ID
-   `_aliyun_arms_alert_type`: 告警类型
-   `_aliyun_arms_alert_level`: 告警等级 |
|Operator|String|eq|选项：

 -   `eq`：等于
-   `re`：匹配正则 |
|Value|String|app|标签取值。 |
|Name|String|Prometheus Alert|分派策略名称。 |
|NotifyRules|Array of NotifyRule| |通知方式。 |
|NotifyChannels|List|email|通知方式：

 -   `dingTalk`
-   `sms`
-   `webhook`
-   `email`
-   `wechat` |
|NotifyObjects|Array of NotifyObject| |通知对象集合。 |
|Name|String|JohnDoe|联系人或联系人组的名称。 |
|NotifyObjectId|String|1|联系人或联系人组的ID。 |
|NotifyType|String|CONTACT|通知方式：

 -   `CONTACT`：联系人
-   `CONTACT_GROUP`：联系人组 |
|RuleId|Long|10282|分派规则ID。 |
|State|String|true|是否启用该分派策略。

 -   `true`：启用
-   `false`：关闭 |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeDispatchRule
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

