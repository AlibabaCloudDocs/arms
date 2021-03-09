# ListIpOrHosts

调用 ListIpOrHosts 获取链路追踪数据中的 IP 地址或者机器名称，可获取整个地域或某个应用下的所有 IP 地址。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=ListIpOrHosts&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListIpOrHosts|系统规定参数，取值为 `ListIpOrHosts`。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为 `cn-beijing` 等。 |
|ServiceName|String|否|service1|应用名称，非必选值。若不为空则只查询此应用下的 IP 地址。 |
|StartTime|Long|否|1583683200000|开始时间。 |
|EndTime|Long|否|1583723776974|结束时间。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IpNames|List|\[ "10.0.0.0", "10.0.0.1" \]|IP 地址列表 |
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListIpOrHosts
&RegionId=cn-beijing
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>23D9757C-CB58-41A5-BBE7-2A9A0652B2F4</RequestId>
<IpNames>
    <IpName>172.19.33.172</IpName>
    <IpName>null</IpName>
    <IpName>10.0.0.5</IpName>
</IpNames>
```

`JSON` 格式

```
{
  "RequestId": "23D9757C-CB58-41A5-BBE7-2A9A0652B2F4",
  "IpNames": {
    "IpName": [
      "172.19.33.172",
      "10.0.0.5"
    ]
  }
}
```

