# GetPrometheusApiToken

调用GetPrometheusApiToken接口获取集成ARMS Prometheus监控所需的Token。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetPrometheusApiToken&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetPrometheusApiToken|系统规定参数，取值为`GetPrometheusApiToken`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1A9C645C-C83F-4C9D-8CCB-29BEC9E1\*\*\*\*|请求ID。 |
|Token|String|6dcbb77ef4ba6ef5466b5debf9e2\*\*\*\*|集成ARMS Prometheus监控所需的Token。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetPrometheusApiToken
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetPrometheusApiTokenResponse>
	  <RequestId>1A9C645C-C83F-4C9D-8CCB-29BEC9E1****</RequestId>
	  <Token>6dcbb77ef4ba6ef5466b5debf9e2****</Token>
</GetPrometheusApiTokenResponse>
```

`JSON` 格式

```
{
    "RequestId": "1A9C645C-C83F-4C9D-8CCB-29BEC9E1****",
    "Token": "6dcbb77ef4ba6ef5466b5debf9e2****"
}
```

