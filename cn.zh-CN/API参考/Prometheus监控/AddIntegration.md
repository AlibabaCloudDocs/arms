# AddIntegration

调用AddIntegration接口集成ARMS Prometheus监控的大盘以及采集规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=AddIntegration&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddIntegration|系统规定参数，取值为`AddIntegration`。 |
|ClusterId|String|是|cc7a37ee31aea4ed1a059eff8034b\*\*\*\*|阿里云容器服务Kubernetes版的Kubernetes集群的ID。 |
|Integration|String|是|asm|ARMS支持的软件缩写。可选值（不区分大小写）：`ASM`、`IoT`和`Flink`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|success|操作是否成功。 |
|RequestId|String|1A9C645C-C83F-4C9D-8CCB-29BEC9E1\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=AddIntegration
&ClusterId=cc7a37ee31aea4ed1a059eff8034b****
&Integration=asm
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<AddIntegrationResponse>
	  <RequestId>1A9C645C-C83F-4C9D-8CCB-29BEC9E1****</RequestId>
	  <Data>success</Data>
</AddIntegrationResponse>
```

`JSON` 格式

```
{
    "RequestId": "1A9C645C-C83F-4C9D-8CCB-29BEC9E1****",
    "Data": "success"
}
```

