# ListPrometheusAlertTemplates

Queries the alert templates of Prometheus Service.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListPrometheusAlertTemplates&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListPrometheusAlertTemplates|The operation that you want to perform. Set the value to ListPrometheusAlertTemplates. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|ClusterId|String|No|c0bad479465464e1d8c1e641b0afb\*\*\*\*|The ID of the cluster. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PrometheusAlertTemplates|Array of PrometheusAlertTemplate| |The struct returned. |
|AlertName|String|The available memory on the node is less than 10%|The name of the alert rule. |
|Annotations|Array of Annotation| |The annotations of the alert rule. |
|Name|String|message|The name of the annotation. |
|Value|String|The available memory on node \{\{ $labels.instance \}\} is less than 10%. Available memory: \{\{ $value \}\}%|The value of the annotation. |
|Description|String|The available memory on node \{\{ $labels.instance \}\} is less than 10%. Available memory: \{\{ $value \}\}%|The message of the alert notification. Tags can be referenced in the \{\{$labels.xxx\}\} format. |
|Duration|String|1m|The duration of the alert. |
|Expression|String|node\_memory\_MemAvailable\_bytes / node\_memory\_MemTotal\_bytes \* 100 < 10|The expression of the alert rule. |
|Labels|Array of Label| |The tags of the alert rule. |
|Name|String|severity|The name of the tag. |
|Value|String|warning|The value of the tag. |
|Type|String|Node|The type of the alert rule. |
|Version|String|1.0|The version of the alert rule. |
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=ListPrometheusAlertTemplates
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListPrometheusAlertTemplatesResponse>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
  <PrometheusAlertTemplates>
        <Type>Node</Type>
        <Description>The available memory on node {{ $labels.instance }} is less than 10%. Available memory: {{ $value }}%</Description>
        <AlertName>The available memory on the node is less than 10%</AlertName>
        <Version>1.0</Version>
        <Expression>node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100 &lt; 10</Expression>
        <Duration>1m</Duration>
        <Labels>
              <Value>warning</Value>
              <Name>severity</Name>
        </Labels>
        <Annotations>
              <Value>The available memory on node {{ $labels.instance }} is less than 10%. Available memory: {{ $value }}%</Value>
              <Name>message</Name>
        </Annotations>
  </PrometheusAlertTemplates>
</ListPrometheusAlertTemplatesResponse>
```

`JSON` format

```
{
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****",
    "PrometheusAlertTemplates": {
        "Type": "Node",
        "Description": "The available memory on node {{ $labels.instance }} is less than 10%. Available memory: {{ $value }}%",
        "AlertName": "The available memory on the node is less than 10%",
        "Version": 1,
        "Expression": "node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100 &lt; 10",
        "Duration": "1m",
        "Labels": {
            "Value": "warning",
            "Name": "severity"
        },
        "Annotations": {
            "Value": "The available memory on node {{ $labels.instance }} is less than 10%. Available memory: {{ $value }}%",
            "Name": "message"
        }
    }
}
```

