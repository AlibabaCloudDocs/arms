# ListPrometheusAlertRules

调用ListPrometheusAlertRules接口查看Prometheus告警规则列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListPrometheusAlertRules&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListPrometheusAlertRules|系统规定参数。取值：ListPrometheusAlertRules。 |
|ClusterId|String|是|c0bad479465464e1d8c1e641b0afb\*\*\*\*|集群ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Name|String|否|Prometheus\_Alert|告警规则名称。 |
|Type|String|否|自定义|告警规则类型。 |
|Status|Integer|否|1|告警规则启用状态，取值：

 -   `1`：开启
-   `0`：关闭 |
|MatchExpressions|String|否|\[\{"key":"severity","value":"critical","operator":"re"\}\]|标签匹配条件的JSON串。关于此字段的详细说明参见下文**关于参数MatchExpressions的补充说明**。 |

## 关于参数**MatchExpressions**的补充说明

**JSON串示例及说明**

```

[
{
    "key":"severity",                           // 标签的Key。
    "value":"critical",                           // 标签的Value。
    "operator":"re"                           // eq：等于；re：匹配正则。
}
]

```

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PrometheusAlertRules|Array of PrometheusAlertRule| |返回结构体。 |
|AlertId|Long|3888704|告警规则ID。 |
|AlertName|String|Prometheus\_Alert|告警规则名称。 |
|Annotations|Array of Annotation| |告警规则的注释。 |
|Name|String|message|注释的名称。 |
|Value|String|$\{\{$labels.pod\_name\}\}CPU使用率大于80%，当前值\{\{$value\}\}%|注释的值。 |
|ClusterId|String|c0bad479465464e1d8c1e641b0afb\*\*\*\*|集群ID。 |
|DispatchRuleId|Long|10282|通知策略ID，当**NotifyType**指定为`DISPATCH_RULE`时显示此参数。 |
|Duration|String|1m|持续时间。 |
|Expression|String|100 \* \(sum\(rate\(container\_cpu\_usage\_seconds\_total\[1m\]\)\) by \(pod\_name\) / sum\(label\_replace\(kube\_pod\_container\_resource\_limits\_cpu\_cores, \\"pod\_name\\", \\"$1\\", \\"pod\\", \\"\(.\*\)\\"\)\) by \(pod\_name\)\)\>75|告警表达式。 |
|Labels|Array of Label| |告警规则的标签。 |
|Name|String|severity|标签的名称。 |
|Value|String|critical|标签的值。 |
|Message|String|$\{\{$labels.pod\_name\}\}CPU使用率大于80%，当前值\{\{$value\}\}%|告警通知消息，支持按照\{\{$labels.xxx\}\}格式来引用标签。 |
|NotifyType|String|ALERT\_MANAGER|通知类型， 取值：

 -   `ALERT_MANAGER`：通过报警运维中心通知。
-   `DISPATCH_RULE`：指定通知策略进行通知。 |
|Status|Integer|1|告警规则启用状态，取值：

 -   `1`：开启
-   `0`：关闭 |
|Type|String|自定义|告警规则类型。 |
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListPrometheusAlertRules
&ClusterId=c0bad479465464e1d8c1e641b0afb****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListPrometheusAlertRulesResponse>
  <PrometheusAlertRules>
        <Status>1</Status>
        <NotifyType>ALERT_MANAGER</NotifyType>
        <Type>自定义</Type>
        <AlertId>3888704</AlertId>
        <AlertName>Prometheus_Alert</AlertName>
        <Message>${{$labels.pod_name}}CPU使用率大于80%，当前值{{$value}}%</Message>
        <ClusterId>c0bad479465464e1d8c1e641b0afb****</ClusterId>
        <Expression>100 * (sum(rate(container_cpu_usage_seconds_total[1m])) by (pod_name) / sum(label_replace(kube_pod_container_resource_limits_cpu_cores, \"pod_name\", \"$1\", \"pod\", \"(.*)\")) by (pod_name))&gt;75</Expression>
        <DispatchRuleId>10282</DispatchRuleId>
        <Duration>1m</Duration>
        <Labels>
              <Value>critical</Value>
              <Name>severity</Name>
        </Labels>
        <Annotations>
              <Value>${{$labels.pod_name}}CPU使用率大于80%，当前值{{$value}}%</Value>
              <Name>message</Name>
        </Annotations>
  </PrometheusAlertRules>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
</ListPrometheusAlertRulesResponse>
```

`JSON`格式

```
{
    "PrometheusAlertRules": {
        "Status": 1,
        "NotifyType": "ALERT_MANAGER",
        "Type": "自定义",
        "AlertId": 3888704,
        "AlertName": "Prometheus_Alert",
        "Message": "${{$labels.pod_name}}CPU使用率大于80%，当前值{{$value}}%",
        "ClusterId": "c0bad479465464e1d8c1e641b0afb****",
        "Expression": "100 * (sum(rate(container_cpu_usage_seconds_total[1m])) by (pod_name) / sum(label_replace(kube_pod_container_resource_limits_cpu_cores, \\\"pod_name\\\", \\\"$1\\\", \\\"pod\\\", \\\"(.*)\\\")) by (pod_name))&gt;75",
        "DispatchRuleId": 10282,
        "Duration": "1m",
        "Labels": {
            "Value": "critical",
            "Name": "severity"
        },
        "Annotations": {
            "Value": "${{$labels.pod_name}}CPU使用率大于80%，当前值{{$value}}%",
            "Name": "message"
        }
    },
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****"
}
```

