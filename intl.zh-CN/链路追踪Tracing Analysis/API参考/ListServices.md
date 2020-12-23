# ListServices

调用 ListServices 获取某个地域下的所有应用列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=xtrace&api=ListServices&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListServices|系统规定参数，取值为 `ListServices`。 |
|RegionId|String|是|cn-beijing|地域 ID，例如杭州填写为 `cn-hangzhou`，北京填写为`cn-beijing` 等。 |
|AppType|String|否|XTRACE|应用类型，非必选值。可填写 `XTRACE` 或不填。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|请求 ID。 |
|Services|Array| |返回的应用列表。 |
|Service| | | |
|Pid|String|123k456@abcc6efc437|应用 ID。 |
|RegionId|String|cn-hangzhou|地域 ID，例如 `cn-hangzhou` 为杭州，`cn-beijing` 为北京等。 |
|ServiceName|String|a3|应用名称。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListServices
&RegionId=cn-beijing
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<Services>
      <Service>
            <ServiceName>a3</ServiceName>
            <Pid>aokcdqn3ly@741623b4e915df8</Pid>
            <RegionId>cn-hangzhou</RegionId>
      </Service>
</Services>
```

`JSON` 格式

```
{
  "Services": {
    "Service": [
      {
        "ServiceName": "a3",
        "Pid": "aokcdqn3ly@741623b4e915df8",
        "RegionId": "cn-hangzhou"
      }
      ]
    }
}
```

