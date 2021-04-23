# ListActivatedAlerts

Queries the alerts that have been triggered.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListActivatedAlerts&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListActivatedAlerts|The operation that you want to perform. Set the value to ListActivatedAlerts. |
|CurrentPage|Integer|Yes|1|The number of the page to return. Default value: `1`. |
|PageSize|Integer|Yes|10|The number of entries to return on each page. Default value: `10`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Filter|String|No|\{"alertname":"The CPU utilization of the container exceeds 80%"\}|The filter condition in the `{"key":"value"}`format. You must specify the `key` and `value` of the filter condition. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Page|Struct| |The struct returned. |
|Alerts|Array of Alert| |The alerts that have been triggered. |
|AlertId|String|3888704|The ID of the alert rule. |
|AlertName|String|The CPU utilization of the container exceeds 80%|The name of the alert rule. |
|AlertType|String|ARMS-Prometheus Service|The type of the alert. |
|Count|Integer|598|The number of times that the alert event was received. |
|CreateTime|Long|1616466300000|The timestamp when the alert rule was created. |
|DispatchRules|Array of DispatchRule| |The notification policies. |
|RuleId|Integer|7021|The ID of the notification policy. |
|RuleName|String|Notification policy for the alert in which the CPU utilization of the container exceeds 80%|The name of the notification policy. |
|EndsAt|Long|1616502540000|The timestamp when the alert was ended. |
|ExpandFields|Map|"severity": "critical", "\_aliyun\_arms\_alert\_level": "ERROR", "pod": "night-test-group-1-1-5f5d6f4d84-pszns", "\_aliyun\_arms\_alert\_type": "101", "\_aliyun\_arms\_integration\_name": "test integration-prometheus", "alertname": "PodRestart\_jiubiantestphp2", "\_aliyun\_arms\_userid": "1131971649496228", "\_aliyun\_arms\_involvedObject\_name": "jiubiantestphp2", "\_aliyun\_arms\_involvedObject\_id": "ccafb2763cfa7415eb2e2a60a74b1f825", "\_aliyun\_arms\_region\_id": "cn-beijing", "\_aliyun\_arms\_involvedObject\_kind": "cluster", "\_aliyun\_arms\_product\_type": "PROMETHEUS", "namespace": "default", "\_aliyun\_arms\_integration\_id": "80", "\_aliyun\_arms\_involvedObject\_type": "ManagedKubernetes", "\_aliyun\_arms\_alert\_rule\_id": "3612229"|The extended fields that indicate the following tags:

 -   The tags that are carried in the metrics of the alert rule expression.
-   The tags that are created based on the alert rule.
-   The default tags of Application Real-Time Monitoring Service \(ARMS\). |
|IntegrationName|String|testphp2|The name of the object that is associated with the alert. |
|IntegrationType|String|PROMETHEUS|The type of the service integration that generated the alert. |
|InvolvedObjectKind|String|cluster|The type of the object that is associated with the alert. |
|InvolvedObjectName|String|test integration-prometheus|The name of the service integration that generated the alert. |
|Message|String|Alert name: PodRestart\_testphp2, \\n Pod night-test-group-1-1-5f5d6f4d84-pszns is restarted. Value: 133.33%, 1.33%|The description of the alert. |
|Severity|String|critical|The level of the alert. Valid values:

 -   `critical`
-   `error`
-   `warn`
-   `page` |
|StartsAt|Long|1616466300000|The timestamp when the alert was generated. |
|Status|String|Active|The status of the alert. Valid values:

 -   `Active`
-   `Inhibited`
-   `Silenced`
-   `Resolved` |
|Page|Integer|1|The page number of the returned page. |
|PageSize|Integer|20|The number of entries returned per page. |
|Total|Integer|5|The total number of entries returned. |
|RequestId|String|BDB74B8F-4123-482A-ABB7-7F440349\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=ListActivatedAlerts
&CurrentPage=1
&PageSize=10
&RegionId=cn-hangzhou	
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListActivatedAlertsResponse>
  <RequestId>BDB74B8F-4123-482A-ABB7-7F440349****</RequestId>
  <Page>
        <PageSize>20</PageSize>
        <Total>5</Total>
        <Page>1</Page>
        <Alerts>
              <Status>Active</Status>
              <AlertName>The CPU utilization of the container exceeds 80%</AlertName>
              <Message>Alert name: PodRestart_testphp2, \n Pod night-test-group-1-1-5f5d6f4d84-pszns is restarted. Value: 133.33%, 1.33%</Message>
              <InvolvedObjectKind>cluster</InvolvedObjectKind>
              <CreateTime>1616466300000</CreateTime>
              <Severity>critical</Severity>
              <Count>598</Count>
              <ExpandFields>       "severity": "critical",           "_aliyun_arms_alert_level": "ERROR",           "pod": "night-test-group-1-1-5f5d6f4d84-pszns",           "_aliyun_arms_alert_type": "101",           "_aliyun_arms_integration_name": "test integration-prometheus",           "alertname": "PodRestart_jiubiantestphp2",           "_aliyun_arms_userid": "1131971649496228",           "_aliyun_arms_involvedObject_name": "jiubiantestphp2",           "_aliyun_arms_involvedObject_id": "ccafb2763cfa7415eb2e2a60a74b1f825",           "_aliyun_arms_region_id": "cn-beijing",           "_aliyun_arms_involvedObject_kind": "cluster",           "_aliyun_arms_product_type": "PROMETHEUS",           "namespace": "default",           "_aliyun_arms_integration_id": "80",           "_aliyun_arms_involvedObject_type": "ManagedKubernetes",           "_aliyun_arms_alert_rule_id": "3612229"</ExpandFields>
              <InvolvedObjectName>test integration-prometheus</InvolvedObjectName>
              <EndsAt>1616502540000</EndsAt>
              <AlertType>ARMS-Prometheus Service</AlertType>
              <IntegrationName>testphp2</IntegrationName>
              <AlertId>3888704</AlertId>
              <StartsAt>1616466300000</StartsAt>
              <IntegrationType>PROMETHEUS</IntegrationType>
              <DispatchRules>
                    <RuleId>7021</RuleId>
                    <RuleName>Notification policy for the alert in which the CPU utilization of the container exceeds 80%</RuleName>
              </DispatchRules>
        </Alerts>
  </Page>
</ListActivatedAlertsResponse>
```

`JSON` format

```
{
    "RequestId": "BDB74B8F-4123-482A-ABB7-7F440349****",
    "Page": {
        "PageSize": 20,
        "Total": 5,
        "Page": 1,
        "Alerts": {
            "Status": "Active",
            "AlertName": "The CPU utilization of the container exceeds 80%",
            "Message": "Alert name: PodRestart_testphp2, \n Pod night-test-group-1-1-5f5d6f4d84-pszns is restarted. Value: 133.33%, 1.33%",
            "InvolvedObjectKind": "cluster",
            "CreateTime": 1616466300000,
            "Severity": "critical",
            "Count": 598,
            "ExpandFields": "\"severity\": \"critical\",           \"_aliyun_arms_alert_level\": \"ERROR\",           \"pod\": \"night-test-group-1-1-5f5d6f4d84-pszns\",           \"_aliyun_arms_alert_type\": \"101\",           \"_aliyun_arms_integration_name\": \"test integration-prometheus\",           \"alertname\": \"PodRestart_jiubiantestphp2\",           \"_aliyun_arms_userid\": \"1131971649496228\",           \"_aliyun_arms_involvedObject_name\": \"jiubiantestphp2\",           \"_aliyun_arms_involvedObject_id\": \"ccafb2763cfa7415eb2e2a60a74b1f825\",           \"_aliyun_arms_region_id\": \"cn-beijing\",           \"_aliyun_arms_involvedObject_kind\": \"cluster\",           \"_aliyun_arms_product_type\": \"PROMETHEUS\",           \"namespace\": \"default\",           \"_aliyun_arms_integration_id\": \"80\",           \"_aliyun_arms_involvedObject_type\": \"ManagedKubernetes\",           \"_aliyun_arms_alert_rule_id\": \"3612229\"",
            "InvolvedObjectName": "test integration-prometheus",
            "EndsAt": 1616502540000,
            "AlertType": "ARMS-Prometheus Service",
            "IntegrationName": "testphp2",
            "AlertId": 3888704,
            "StartsAt": 1616466300000,
            "IntegrationType": "PROMETHEUS",
            "DispatchRules": {
                "RuleId": 7021,
                "RuleName": "Notification policy for the alert in which the CPU utilization of the container exceeds 80%"
            }
        }
    }
}
```

