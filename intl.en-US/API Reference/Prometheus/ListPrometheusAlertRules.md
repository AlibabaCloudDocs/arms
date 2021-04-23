# ListPrometheusAlertRules

Queries the alert rules of Prometheus Service.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListPrometheusAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListPrometheusAlertRules|The operation that you want to perform. Set the value to ListPrometheusAlertRules. |
|ClusterId|String|Yes|c0bad479465464e1d8c1e641b0afb\*\*\*\*|The ID of the cluster. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Name|String|No|Prometheus\_Alert|The name of the alert rule. |
|Type|String|No|Custom|The type of the alert rule. |
|Status|Integer|No|1|Specifies whether the alert rule is enabled. Valid values:

 -   `1`: The alert rule is enabled.
-   `0`: The alert rule is disabled. |
|MatchExpressions|String|No|\[\{"key":"severity","value":"critical","operator":"re"\}\]|The tag match conditions that are described in a JSON string. For more information about this parameter, see the **Supplementary description about the MatchExpressions parameter** section. |

## Supplementary description about the **MatchExpressions** parameter

**Sample JSON string and description**

```

[
{
    "key":"severity",                           // The key of the tag. 
    "value":"critical",                           // the Value of the tag. 
    "operator":"re"                           // eq: equal to. re: matches a regular expression. 
}
]

```

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PrometheusAlertRules|Array of PrometheusAlertRule| |The struct returned. |
|AlertId|Long|3888704|The ID of the alert rule. |
|AlertName|String|Prometheus\_Alert|The name of the alert rule. |
|Annotations|Array of Annotation| |The annotations of the alert rule. |
|Name|String|message|The name of the annotation. |
|Value|String|The CPU utilization of $\{\{$labels.pod\_name\}\} exceeds 80%. Current value: \{\{$value\}\}%|The value of the annotation. |
|ClusterId|String|c0bad479465464e1d8c1e641b0afb\*\*\*\*|The ID of the cluster. |
|DispatchRuleId|Long|10282|The ID of the notification policy. This parameter is available when the value of the **NotifyType** parameter is `DISPATCH_RULE`. |
|Duration|String|1m|The duration of the alert. |
|Expression|String|100 \* \(sum\(rate\(container\_cpu\_usage\_seconds\_total\[1m\]\)\) by \(pod\_name\) / sum\(label\_replace\(kube\_pod\_container\_resource\_limits\_cpu\_cores, \\"pod\_name\\", \\"$1\\", \\"pod\\", \\"\(.\*\)\\"\)\) by \(pod\_name\)\)\>75|The expression of the alert rule. |
|Labels|Array of Label| |The tags of the alert rule. |
|Name|String|severity|The name of the tag. |
|Value|String|critical|The value of the tag. |
|Message|String|The CPU utilization of $\{\{$labels.pod\_name\}\} exceeds 80%. Current value: \{\{$value\}\}%|The message of the alert notification. Tags can be referenced in the \{\{$labels.xxx\}\} format. |
|NotifyType|String|ALERT\_MANAGER|The method of sending the alert notification. Valid values:

 -   `ALERT_MANAGER`: The alert notification is sent by Operation Center.
-   `DISPATCH_RULE`: The alert notification is sent based on the specified notification policy. |
|Status|Integer|1|Indicates whether the alert rule is enabled. Valid values:

 -   `1`: The alert rule is enabled.
-   `0`: The alert rule is disabled. |
|Type|String|Custom|The type of the alert rule. |
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=ListPrometheusAlertRules
&ClusterId=c0bad479465464e1d8c1e641b0afb****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListPrometheusAlertRulesResponse>
  <PrometheusAlertRules>
        <Status>1</Status>
        <NotifyType>ALERT_MANAGER</NotifyType>
        <Type>Custom</Type>
        <AlertId>3888704</AlertId>
        <AlertName>Prometheus_Alert</AlertName>
        <Message>The CPU utilization of ${{$labels.pod_name}} exceeds 80%. Current value: {{$value}}%</Message>
        <ClusterId>c0bad479465464e1d8c1e641b0afb****</ClusterId>
        <Expression>100 * (sum(rate(container_cpu_usage_seconds_total[1m])) by (pod_name) / sum(label_replace(kube_pod_container_resource_limits_cpu_cores, \"pod_name\", \"$1\", \"pod\", \"(.*)\")) by (pod_name))&gt;75</Expression>
        <DispatchRuleId>10282</DispatchRuleId>
        <Duration>1m</Duration>
        <Labels>
              <Value>critical</Value>
              <Name>severity</Name>
        </Labels>
        <Annotations>
              <Value>The CPU utilization of ${{$labels.pod_name}} exceeds 80%. Current value: {{$value}}%</Value>
              <Name>message</Name>
        </Annotations>
  </PrometheusAlertRules>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
</ListPrometheusAlertRulesResponse>
```

`JSON` format

```
{
    "PrometheusAlertRules": {
        "Status": 1,
        "NotifyType": "ALERT_MANAGER",
        "Type": "Custom",
        "AlertId": 3888704,
        "AlertName": "Prometheus_Alert",
        "Message": "The CPU utilization of ${{$labels.pod_name}} exceeds 80%. Current value: {{$value}}%",
        "ClusterId": "c0bad479465464e1d8c1e641b0afb****",
        "Expression": "100 * (sum(rate(container_cpu_usage_seconds_total[1m])) by (pod_name) / sum(label_replace(kube_pod_container_resource_limits_cpu_cores, \\\"pod_name\\\", \\\"$1\\\", \\\"pod\\\", \\\"(.*)\\\")) by (pod_name))&gt;75",
        "DispatchRuleId": 10282,
        "Duration": "1m",
        "Labels": {
            "Value": "critical",
            "Name": "severity"
        },
        "Annotations": {
            "Value": "The CPU utilization of ${{$labels.pod_name}} exceeds 80%. Current value: {{$value}}%",
            "Name": "message"
        }
    },
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****"
}
```

