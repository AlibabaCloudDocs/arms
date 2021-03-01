# CreateDispatchRule

调用CreateDispatchRule接口创建分派策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=CreateDispatchRule&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDispatchRule|系统规定参数。取值：CreateDispatchRule。 |
|DispatchRule|String|是|\{ "system": false, "ruleid": 10282, "name": "Prometheus Alert", "labelMatchExpressionGrid": \{ "labelMatchExpressionGroups": \[ \{ "labelMatchExpressions": \[ \{ "key": "\_aliyun\_arms\_involvedObject\_kind", "value": "app", "operator": "eq" \} \] \} \] \}, "dispatchType": "CREATE\_ALERT/DISCARD\_ALERT", "isRecover": true, "groupRules": \[ \{ "groupId": 1, "groupingFields": \[ "alertname" \], "groupWait": 10, "groupInterval": 15, "repeatInterval": 20 \} \], "notifyRules": \[ \{ "notifyObjects": \[ \{ "notifyType": "ARMS\_CONTACT", "name": "JohnDoe", "notifyObjectId": 1 \}, \{ "notifyType": "ARMS\_CONTACT\_GROUP", "name": "JohnDoe\_group", "notifyObjectId": 2 \} \], "notifyChannels":\["dingTalk","wechat","webhook","email"\] \}, \], \}|分派条件的配置JSON串。关于此字段的详细说明参见下文**关于参数DispatchRule的补充说明**。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 关于参数**DispatchRule**的补充说明

**JSON串示例及说明**

```

{
  "system": false,        //分派条件是否可编辑。true：不可编辑；false：可编辑。
  "ruleid": 10282,           //分派规则ID。
  "name": "Prometheus Alert",   //分派策略名称。
  "labelMatchExpressionGrid": {
    "labelMatchExpressionGroups": [     //设置分派条件。
      {
        "labelMatchExpressions": [
          {
            "key": "_aliyun_arms_involvedObject_kind",   //分派条件标签，详见下一节。
            "value": "app",                              //标签取值。
            "operator": "eq"                             //eq：等于；re：匹配正则。
          }
        ]
      }
    ]
  },
  "dispatchType": "CREATE_ALERT/DISCARD_ALERT",    //告警处理方式。CREATE_ALERT：就是生成报警；DISCARD_ALERT：丢弃报警事件，即不告警。
  "isRecover": true,               //是否发送恢复的告警。true：发送；false：不发送。
  "groupRules": [                  //设置事件分组。
    {
      "groupId": 1,               //分组ID。
      "groupingFields": [         //指定相同字段内容的事件分到一个组：设置分组字段，相同字段的告警内容会分别通过独立信息发送给处理人。
        "alertname"
      ],
      "groupWait": 10,                 //分组等待时间：收到第一个告警后会等待设置的时间，等待分组时间后收到的所有告警会以一条信息发送给处理人。
      "groupInterval": 15,             //分组间隔时间：在重复告警静默时间内，如果有新告警产生，等待设置的时间后就会直接发送新的告警信息。
      "repeatInterval": 20             //重复告警静默时间：所有告警会以设置的时间间隔循环发送告警信息直至告警消失。
    }
  ],
  "notifyRules": [            //设置通知规则。
    {
      "notifyObjects": [
        {
          "notifyType": "ARMS_CONTACT",     //ARMS_CONTACT：联系人；ARMS_CONTACT_GROUP：联系人组。
          "name": "JohnDoe",                //联系人或联系人组的名称。
          "notifyObjectId": 1               //联系人或联系人组的ID。
        },
        {
          "notifyType": "ARMS_CONTACT_GROUP",
          "name": "JohnDoe_group",
          "notifyObjectId": 2
        }
      ],
      "notifyChannels":["dingTalk","wechat","webhook","email"]     //通知方式：dingTalk（ 钉钉）、sms（短信）、webhook、email（邮件）、wechat（微信）。
    },
  ],
}

```

**分派标签取值枚举**

-   `_aliyun_arms_userid` : 用户ID
-   `_aliyun_arms_involvedObject_kind`: 关联对象类型
-   `_aliyun_arms_involvedObject_id`: 关联对象ID
-   `_aliyun_arms_involvedObject_name`: 关联对象名称
-   `_aliyun_arms_alert_name`: 告警名称
-   `_aliyun_arms_alert_rule_id`: 告警规则对应的ID
-   `_aliyun_arms_alert_type`: 告警类型
-   `_aliyun_arms_alert_level`: 告警等级

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DispatchRuleId|Long|10413|分派策略ID。 |
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateDispatchRule
&DispatchRule=
{
  "system": false,
  "ruleid": 10282,
  "name": "Prometheus Alert",
  "labelMatchExpressionGrid": {
    "labelMatchExpressionGroups": [
      {
        "labelMatchExpressions": [
          {
            "key": "_aliyun_arms_involvedObject_kind",
            "value": "app",
            "operator": "eq"
          }
        ]
      }
    ]
  },
  "dispatchType": "CREATE_ALERT/DISCARD_ALERT",
  "isRecover": true,
  "groupRules": [
    {
      "groupId": 1,
      "groupingFields": [
        "alertname"
      ],
      "groupWait": 10,
      "groupInterval": 15,
      "repeatInterval": 20
    }
  ],
  "notifyRules": [
    {
      "notifyObjects": [
        {
          "notifyType": "ARMS_CONTACT",
          "name": "JohnDoe",
          "notifyObjectId": 1
        },
        {
          "notifyType": "ARMS_CONTACT_GROUP",
          "name": "JohnDoe_group",
          "notifyObjectId": 2
        }
      ],
      "notifyChannels":["dingTalk","wechat","webhook","email"]
    },
  ],
}
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateDispatchRuleResponse>
      <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C****</RequestId>
      <DispatchRuleId>10413</DispatchRuleId>
</CreateDispatchRuleResponse>
```

`JSON`格式

```
{
    "RequestId": "A5EC8221-08F2-4C95-9AF1-49FD998C****",
    "DispatchRuleId": 10413
}
```

