# ListPrometheusAlertTemplates

调用ListPrometheusAlertTemplates接口查看Prometheus告警模板列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListPrometheusAlertTemplates&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListPrometheusAlertTemplates|系统规定参数。取值：ListPrometheusAlertTemplates。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|ClusterId|String|否|c0bad479465464e1d8c1e641b0afb\*\*\*\*|集群ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PrometheusAlertTemplates|Array of PrometheusAlertTemplate| |返回结构体。 |
|AlertName|String|节点内存可用率不足10%|告警规则名称。 |
|Annotations|Array of Annotation| |告警规则的注释。 |
|Name|String|message|注释的名称。 |
|Value|String|节点 \{\{ $labels.instance \}\} 可用内存不足10%，当前可用内存 \{\{ $value \}\}%|注释的值。 |
|Description|String|节点 \{\{ $labels.instance \}\} 可用内存不足10%，当前可用内存 \{\{ $value \}\}%|告警消息，支持按照\{\{$labels.xxx\}\}格式来引用标签。 |
|Duration|String|1m|持续时间。 |
|Expression|String|node\_memory\_MemAvailable\_bytes / node\_memory\_MemTotal\_bytes \* 100 < 10|告警表达式。 |
|Labels|Array of Label| |告警规则的标签。 |
|Name|String|severity|标签的名称。 |
|Value|String|warning|标签的值。 |
|Type|String|节点|告警规则类型。 |
|Version|String|1.0|告警规则版本。 |
|RequestId|String|9FEA6D00-317F-45E3-9004-7FB8B0B7\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListPrometheusAlertTemplates
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListPrometheusAlertTemplatesResponse>
  <RequestId>9FEA6D00-317F-45E3-9004-7FB8B0B7****</RequestId>
  <PrometheusAlertTemplates>
        <Type>节点</Type>
        <Description>节点 {{ $labels.instance }} 可用内存不足10%，当前可用内存 {{ $value }}%</Description>
        <AlertName>节点内存可用率不足10%</AlertName>
        <Version>1.0</Version>
        <Expression>node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100 &lt; 10</Expression>
        <Duration>1m</Duration>
        <Labels>
              <Value>warning</Value>
              <Name>severity</Name>
        </Labels>
        <Annotations>
              <Value>节点 {{ $labels.instance }} 可用内存不足10%，当前可用内存 {{ $value }}%</Value>
              <Name>message</Name>
        </Annotations>
  </PrometheusAlertTemplates>
</ListPrometheusAlertTemplatesResponse>
```

`JSON`格式

```
{
    "RequestId": "9FEA6D00-317F-45E3-9004-7FB8B0B7****",
    "PrometheusAlertTemplates": {
        "Type": "节点",
        "Description": "节点 {{ $labels.instance }} 可用内存不足10%，当前可用内存 {{ $value }}%",
        "AlertName": "节点内存可用率不足10%",
        "Version": 1,
        "Expression": "node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100 &lt; 10",
        "Duration": "1m",
        "Labels": {
            "Value": "warning",
            "Name": "severity"
        },
        "Annotations": {
            "Value": "节点 {{ $labels.instance }} 可用内存不足10%，当前可用内存 {{ $value }}%",
            "Name": "message"
        }
    }
}
```

