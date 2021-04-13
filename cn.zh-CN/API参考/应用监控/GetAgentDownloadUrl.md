# GetAgentDownloadUrl

调用GetAgentDownloadUrl接口获取探针下载链接。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=GetAgentDownloadUrl&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetAgentDownloadUrl|系统规定参数。取值：GetAgentDownloadUrl。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ArmsAgentDownloadUrl|String|http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/|探针下载链接。 |
|RequestId|String|14043452-D486-4EA1-80C9-BA73FB81\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetAgentDownloadUrl
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetAgentDownloadUrlResponse>
  <ArmsAgentDownloadUrl>http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/</ArmsAgentDownloadUrl>
  <RequestId>14043452-D486-4EA1-80C9-BA73FB81****</RequestId>
</GetAgentDownloadUrlResponse>
```

`JSON`格式

```
{
    "ArmsAgentDownloadUrl": "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/2.7.1.1/",
    "RequestId": "14043452-D486-4EA1-80C9-BA73FB81****"
}
```

