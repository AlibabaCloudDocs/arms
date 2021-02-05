# DeleteScenario

调用DeleteScenario接口删除业务监控。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteScenario&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteScenario|系统规定参数。取值：DeleteScenario。 |
|ScenarioId|Long|是|132|业务监控ID，可通过ListScenario接口获取。 |
|RegionId|String|否|cn-zhangjaikou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|EA24D522-AD35-47B8-8CB2-ADBC382B\*\*\*\*|请求ID。 |
|Result|Boolean|true|是否删除成功。

 -   `true`：删除成功。
-   `false`：删除失败。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteScenario
&ScenarioId=132
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteScenarioResponse>
      <RequestId>EA24D522-AD35-47B8-8CB2-ADBC382B****</RequestId>
      <Result>true</Result>
</DeleteScenarioResponse>
```

`JSON`格式

```
{
    "RequestId": "EA24D522-AD35-47B8-8CB2-ADBC382B****",
    "Result": true
}
```

