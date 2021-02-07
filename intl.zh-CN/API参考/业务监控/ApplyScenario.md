# ApplyScenario

调用ApplyScenario接口创建或更新业务监控。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ApplyScenario&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ApplyScenario|系统规定参数。取值：ApplyScenario。 |
|AppId|String|是|b590lhguqs@28f515462f\*\*\*\*\*\*|应用ID。 |
|Config|Json|是|\{"rpcType":"0","nameMatchType":"EQUALS","service":"/api/pop/test","operator":"and","filterItems":\[\{"type":"HttpHeaders","key":"uid","opt":"==","value":"123456789"\}\],"group":\{"type":"HttpRequestParameters","key":"name"\}\}|业务监控配置JSON字段。关于此字段的详细说明参见下文关于参数**Config**的补充说明。 |
|Name|String|是|测试POP业务监控|业务监控名称。 |
|UpdateOption|Boolean|是|false|是否更新操作。

 -   `true`：更新操作。
-   `false`：插入操作。 |
|RegionId|String|否|cn-zhangjaikou|地域ID。 |
|Scenario|String|否|USER-DEFINED|使用场景。选项：

 -   `USER-DEFINED`（默认）：用户自定义。
-   `EDAS-ROLLOUT`：EDAS应用发布。
-   `OAM-ROLLOUT`：OAM应用发布。
-   `MSC-CANARY`：MSE金丝雀发布。 |
|Sign|String|否|a9f8\*\*\*\*|场景编码。新建业务监控时无需设置，更新业务监控时必须设置。 |
|SnTransfer|Boolean|否|false|染色标是否向下透传。

 -   `true`
-   `false`（默认） |
|SnStat|Boolean|否|false|染色标是否统计流量。

 -   `true`
-   `false`（默认） |
|SnDump|Boolean|否|false|染色标的链路是否Dump业务参数。

 -   `true`
-   `false`（默认） |
|SnForce|Boolean|否|false|染色标的链路是否全量采集。

 -   `true`
-   `false`（默认） |

## 关于参数**Config**的补充说明

**JSON串示例及说明**

```

{
    "rpcType":"0",   //服务类型。0：HTTP入口；255：Kubernete Pod Metadata。
    "nameMatchType":"EQUALS",    //服务名称匹配规则。EQUALS：等于；STARTSWITH：开始等于；CONTAINS：包含；ENDSWITH：结束等于；PATTERNS：模式匹配。
    "service":"/api/pop/test",      //服务名称。
    "operator":"and",    //过滤规则关系。 and：同时满足规则；or：满足任一规则。
    "filterItems":    //过滤规则。
        [{
            "type":"HttpHeaders",    //过滤规则匹配参数，详见下一节。
            "key":"uid",    //过滤字段匹配Key值。
            "opt":"==",    //匹配方式。支持==、!=和contains。
            "value":"123456789"    //过滤字段阈值。
        }],
    "group":    //分组规则。
        {
            "type":"HttpRequestParameters",    //分组规则匹配参数，详见下一节。
            "key":"name"    //分组规则匹配Key值。
        }
}

```

**过滤规则匹配参数**

当服务类型设置为rpcType=0（即HTTP入口）时的匹配参数：

-   HttpRequestParameters
-   HttpHeaders
-   HttpCookies
-   HttpMethod
-   HttpPathVariables

当服务类型设置为rpcType=255（即Kubernete Pod Metadata）时的匹配参数：

-   k8sPodLabel
-   k8sPodAnnotation
-   k8sPodName
-   k8sPodNamespace
-   k8sPodUID
-   k8sPodIp
-   k8sPodServiceAccount

**分组规则匹配参数**

当服务类型设置为rpcType=0（即HTTP入口）时的匹配参数：

-   HttpRequestParameters
-   HttpHeaders
-   HttpCookies
-   HttpMethod
-   HttpPathVariables

当服务类型设置为rpcType=255（即Kubernete Pod Metadata）时的匹配参数：

-   k8sPodLabel
-   k8sPodAnnotation
-   k8sPodName
-   k8sPodNamespace
-   k8sPodUID
-   k8sPodIp
-   k8sPodServiceAccount

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|EA24D522-AD35-47B8-8CB2-ADBC38\*\*\*\*\*\*|请求ID。 |
|Result|String|2b97\*\*\*\*|场景编码，即染色标。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ApplyScenario
&AppId=b590lhguqs@28f515462f******
&Config=
{
    "rpcType":"0",
    "nameMatchType":"EQUALS",
    "service":"/api/pop/test",
    "operator":"and",
    "filterItems":
        [{
            "type":"HttpHeaders",
            "key":"uid",
            "opt":"==",
            "value":"123456789"
        }],
    "group":
        {
            "type":"HttpRequestParameters",
            "key":"name"
        }
}
&Name=测试POP业务监控
&Sign=a9f8****
&UpdateOption=false
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ApplyScenarioResponse>
      <RequestId>EA24D522-AD35-47B8-8CB2-ADBC38******</RequestId>
      <Result>2b97****</Result>
</ApplyScenarioResponse>
```

`JSON`格式

```
{
    "RequestId": "EA24D522-AD35-47B8-8CB2-ADBC38******",
    "Result": "2b97****"
}
```

