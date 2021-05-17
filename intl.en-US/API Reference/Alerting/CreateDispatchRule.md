# CreateDispatchRule

Creates a dispatch policy.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=CreateDispatchRule&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDispatchRule|The operation that you want to perform. Set the value to CreateDispatchRule. |
|DispatchRule|String|Yes|\{ "system": false, "ruleid": 10282, "name": "Prometheus Alert", "labelMatchExpressionGrid": \{ "labelMatchExpressionGroups": \[ \{ "labelMatchExpressions": \[ \{ "key": "\_aliyun\_arms\_involvedObject\_kind", "value": "app", "operator": "eq" \} \] \} \] \}, "dispatchType": "CREATE\_ALERT/DISCARD\_ALERT", "isRecover": true, "groupRules": \[ \{ "groupId": 1, "groupingFields": \[ "alertname" \], "groupWait": 10, "groupInterval": 15, "repeatInterval": 20 \} \], "notifyRules": \[ \{ "notifyObjects": \[ \{ "notifyType": "ARMS\_CONTACT", "name": "JohnDoe", "notifyObjectId": 1 \}, \{ "notifyType": "ARMS\_CONTACT\_GROUP", "name": "JohnDoe\_group", "notifyObjectId": 2 \} \], "notifyChannels":\["dingTalk","wechat","webhook","email"\] \}, \], \}|The dispatch rule configuration. The value is a JSON string. For more information about this parameter, see the following **additional information about the DispatchRule parameter**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Additional information about the **DispatchRule** parameter

**JSON string example and description**

```

{
  "system": false,        // Specifies whether the dispatch rule is editable. Valid values: true: not editable. false: editable. 
  "ruleid": 10282,           // The ID of the dispatch rule. 
  "name": "Prometheus Alert",   // The name of the dispatch policy. 
  "labelMatchExpressionGrid": {
    "labelMatchExpressionGroups": [     // Sets the dispatch rule. 
      {
        "labelMatchExpressions": [
          {
            "key": "_aliyun_arms_involvedObject_kind", // The key of the tag of the dispatch rule. For more information, see the next section. 
            "value": "app",                              // The value of the tag. 
            "operator": "eq"                             // The operator used in the dispatch rule. Valid values: eq: equals to. re: matches a regular expression. 
          }
        ]
      }
    ]
  },
  "dispatchType": "CREATE_ALERT/DISCARD_ALERT",    // The alert handling method. Valid values: CREATE_ALERT: generates an alert. DISCARD_ALERT: discards the alert event and generates no alert. 
  "isRecover": true,               // Specifies whether to send the restored alert. Valid values: true: sends the alert. false: does not send the alert. 
  "groupRules": [                  // Sets the event group. 
    {
      "groupId": 1,               // The ID of the group. 
      "groupingFields": [         // The fields that are used to group events. Events with the same field content are assigned to a group. Alerts with the same specified grouping field are sent to the handler in separate notifications. 
        "alertname"
      ],
      "groupWait": 10,                 // The duration for which the system waits after the first alert is sent. After the duration, all alerts are sent in a single notification to the handler. 
      "groupInterval": 15,             // The grouping interval. During the silence period of repeated alerts, if new alerts are generated, they will be sent after the group waiting time. 
      "repeatInterval": 20             // The silence period of repeated alerts. All alerts are repeatedly sent at specified intervals until the alerts are cleared. 
    }
  ],
  "notifyRules": [            // Sets the notification rule. 
    {
      "notifyObjects": [
        {
          "notifyType": "ARMS_CONTACT",     // The type of the alert contact. Valid values: ARMS_CONTACT: contact. ARMS_CONTACT_GROUP: contact group. 
          "name": "JohnDoe",                // The name of the contact or contact group. 
          "notifyObjectId": 1               // The ID of the contact or contact group. 
        },
        {
          "notifyType": "ARMS_CONTACT_GROUP",
          "name": "JohnDoe_group",
          "notifyObjectId": 2
        }
      ],
      "notifyChannels":["dingTalk","wechat","webhook","email"]     // The notification method. Valid values: dingTalk, sms, webhook, email, and wechat. 
    },
  ],
}

```

**Enumerated keys of the tag of the dispatch rule**

-   `_aliyun_arms_userid`: user ID
-   `_aliyun_arms_involvedObject_kind`: type of the associated object
-   `_aliyun_arms_involvedObject_id`: ID of the associated object
-   `_aliyun_arms_involvedObject_name`: name of the associated object
-   `_aliyun_arms_alert_name`: alert name
-   `_aliyun_arms_alert_rule_id`: alert rule ID
-   `_aliyun_arms_alert_type`: alert type
-   `_aliyun_arms_alert_level`: alert severity

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DispatchRuleId|Long|10413|The ID of the dispatch policy. |
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C\*\*\*\*|The ID of the request. |

## Examples

Sample requests

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
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDispatchRuleResponse>
      <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C****</RequestId>
      <DispatchRuleId>10413</DispatchRuleId>
</CreateDispatchRuleResponse>
```

`JSON` format

```
{
    "RequestId": "A5EC8221-08F2-4C95-9AF1-49FD998C****",
    "DispatchRuleId": 10413
}
```

