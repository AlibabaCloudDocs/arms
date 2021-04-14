# ListActivatedAlerts

调用ListActivatedAlerts接口查询已经触发的告警列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListActivatedAlerts&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListActivatedAlerts|系统规定参数。取值：ListActivatedAlerts。 |
|CurrentPage|Integer|是|1|查询结果分页的页码。默认为`1`。 |
|PageSize|Integer|是|10|查询结果分页的每页项目数量。默认为`10`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Filter|String|否|\{"alertname":"容器CPU使用率大于80%"\}|筛选条件，格式为`{"key":"value"}`。需要设置筛选条件的`key`和`value`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Page|Struct| |返回结构体。 |
|Alerts|Array of Alert| |告警信息。 |
|AlertId|String|3888704|告警规则ID。 |
|AlertName|String|容器CPU使用率大于80%|告警规则名称。 |
|AlertType|String|ARMS-Prometheus监控|告警类型。 |
|Count|Integer|598|告警事件接受次数。 |
|CreateTime|Long|1616466300000|告警规则创建时间的时间戳。 |
|DispatchRules|Array of DispatchRule| |通知策略。 |
|RuleId|Integer|7021|通知策略ID。 |
|RuleName|String|容器CPU使用率大于80%的通知策略|通知策略名称。 |
|EndsAt|Long|1616502540000|告警结束时间。 |
|ExpandFields|Map|"severity": "critical", "\_aliyun\_arms\_alert\_level": "ERROR", "pod": "night-test-group-1-1-5f5d6f4d84-pszns", "\_aliyun\_arms\_alert\_type": "101", "\_aliyun\_arms\_integration\_name": "测试集成-prometheus", "alertname": "PodRestart\_jiubiantestphp2", "\_aliyun\_arms\_userid": "1131971649496228", "\_aliyun\_arms\_involvedObject\_name": "jiubiantestphp2", "\_aliyun\_arms\_involvedObject\_id": "ccafb2763cfa7415eb2e2a60a74b1f825", "\_aliyun\_arms\_region\_id": "cn-beijing", "\_aliyun\_arms\_involvedObject\_kind": "cluster", "\_aliyun\_arms\_product\_type": "PROMETHEUS", "namespace": "default", "\_aliyun\_arms\_integration\_id": "80", "\_aliyun\_arms\_involvedObject\_type": "ManagedKubernetes", "\_aliyun\_arms\_alert\_rule\_id": "3612229"|扩展字段（标签），标签来源包括：

 -   报警规则表达式指标中携带的标签。
-   通过报警规则创建的标签。
-   ARMS系统自带的默认标签。 |
|IntegrationName|String|testphp2|告警关联对象名称。 |
|IntegrationType|String|PROMETHEUS|告警来源集成的类型。 |
|InvolvedObjectKind|String|cluster|告警关联对象类型。 |
|InvolvedObjectName|String|测试集成-prometheus|告警来源集成的名称。 |
|Message|String|报警名称：PodRestart\_testphp2，\\n Pod night-test-group-1-1-5f5d6f4d84-pszns is restart, Value: 133.33%, 1.33%|告警描述信息。 |
|Severity|String|critical|告警等级。取值：

 -   `critical`：严重。
-   `error`：错误。
-   `warn`：警告。
-   `page`：通知。 |
|StartsAt|Long|1616466300000|告警开始时间。 |
|Status|String|Active|告警状态。取值：

 -   `Active`：未恢复。
-   `Inhibited`：抑制。
-   `Silenced`：静默。
-   `Resolved`：已恢复。 |
|Page|Integer|1|查询结果分页页码。 |
|PageSize|Integer|20|查询结果分页的每页项目数量。 |
|Total|Integer|5|查询结果总数。 |
|RequestId|String|BDB74B8F-4123-482A-ABB7-7F440349\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListActivatedAlerts
&CurrentPage=1
&PageSize=10
&RegionId=cn-hangzhou	
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListActivatedAlertsResponse>
  <RequestId>BDB74B8F-4123-482A-ABB7-7F440349****</RequestId>
  <Page>
        <PageSize>20</PageSize>
        <Total>5</Total>
        <Page>1</Page>
        <Alerts>
              <Status>Active</Status>
              <AlertName>容器CPU使用率大于80%</AlertName>
              <Message>报警名称：PodRestart_testphp2，\n Pod night-test-group-1-1-5f5d6f4d84-pszns is restart, Value: 133.33%, 1.33%</Message>
              <InvolvedObjectKind>cluster</InvolvedObjectKind>
              <CreateTime>1616466300000</CreateTime>
              <Severity>critical</Severity>
              <Count>598</Count>
              <ExpandFields>       "severity": "critical",           "_aliyun_arms_alert_level": "ERROR",           "pod": "night-test-group-1-1-5f5d6f4d84-pszns",           "_aliyun_arms_alert_type": "101",           "_aliyun_arms_integration_name": "测试集成-prometheus",           "alertname": "PodRestart_jiubiantestphp2",           "_aliyun_arms_userid": "1131971649496228",           "_aliyun_arms_involvedObject_name": "jiubiantestphp2",           "_aliyun_arms_involvedObject_id": "ccafb2763cfa7415eb2e2a60a74b1f825",           "_aliyun_arms_region_id": "cn-beijing",           "_aliyun_arms_involvedObject_kind": "cluster",           "_aliyun_arms_product_type": "PROMETHEUS",           "namespace": "default",           "_aliyun_arms_integration_id": "80",           "_aliyun_arms_involvedObject_type": "ManagedKubernetes",           "_aliyun_arms_alert_rule_id": "3612229"</ExpandFields>
              <InvolvedObjectName>测试集成-prometheus</InvolvedObjectName>
              <EndsAt>1616502540000</EndsAt>
              <AlertType>ARMS-Prometheus监控</AlertType>
              <IntegrationName>testphp2</IntegrationName>
              <AlertId>3888704</AlertId>
              <StartsAt>1616466300000</StartsAt>
              <IntegrationType>PROMETHEUS</IntegrationType>
              <DispatchRules>
                    <RuleId>7021</RuleId>
                    <RuleName>容器CPU使用率大于80%的通知策略</RuleName>
              </DispatchRules>
        </Alerts>
  </Page>
</ListActivatedAlertsResponse>
```

`JSON`格式

```
{
    "RequestId": "BDB74B8F-4123-482A-ABB7-7F440349****",
    "Page": {
        "PageSize": 20,
        "Total": 5,
        "Page": 1,
        "Alerts": {
            "Status": "Active",
            "AlertName": "容器CPU使用率大于80%",
            "Message": "报警名称：PodRestart_testphp2，\\n Pod night-test-group-1-1-5f5d6f4d84-pszns is restart, Value: 133.33%, 1.33%",
            "InvolvedObjectKind": "cluster",
            "CreateTime": 1616466300000,
            "Severity": "critical",
            "Count": 598,
            "ExpandFields": "\"severity\": \"critical\",           \"_aliyun_arms_alert_level\": \"ERROR\",           \"pod\": \"night-test-group-1-1-5f5d6f4d84-pszns\",           \"_aliyun_arms_alert_type\": \"101\",           \"_aliyun_arms_integration_name\": \"测试集成-prometheus\",           \"alertname\": \"PodRestart_jiubiantestphp2\",           \"_aliyun_arms_userid\": \"1131971649496228\",           \"_aliyun_arms_involvedObject_name\": \"jiubiantestphp2\",           \"_aliyun_arms_involvedObject_id\": \"ccafb2763cfa7415eb2e2a60a74b1f825\",           \"_aliyun_arms_region_id\": \"cn-beijing\",           \"_aliyun_arms_involvedObject_kind\": \"cluster\",           \"_aliyun_arms_product_type\": \"PROMETHEUS\",           \"namespace\": \"default\",           \"_aliyun_arms_integration_id\": \"80\",           \"_aliyun_arms_involvedObject_type\": \"ManagedKubernetes\",           \"_aliyun_arms_alert_rule_id\": \"3612229\"",
            "InvolvedObjectName": "测试集成-prometheus",
            "EndsAt": 1616502540000,
            "AlertType": "ARMS-Prometheus监控",
            "IntegrationName": "testphp2",
            "AlertId": 3888704,
            "StartsAt": 1616466300000,
            "IntegrationType": "PROMETHEUS",
            "DispatchRules": {
                "RuleId": 7021,
                "RuleName": "容器CPU使用率大于80%的通知策略"
            }
        }
    }
}
```

