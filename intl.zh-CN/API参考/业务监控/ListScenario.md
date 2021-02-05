# ListScenario

调用ListScenario接口获取业务监控详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListScenario&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListScenario|系统规定参数。取值：ListScenario。 |
|AppId|String|是|b590lhguqs@28f515462\*\*\*\*\*\*|应用ID。 |
|Name|String|是|测试业务监控|业务监控名称。 |
|RegionId|String|否|cn-zhangjaikou|地域ID。 |
|Scenario|String|否|USER-DEFINED|使用场景。选项：

 -   `USER-DEFINED`（默认）：用户自定义。
-   `EDAS-ROLLOUT`：EDAS应用发布。
-   `OAM-ROLLOUT`：OAM应用发布。
-   `MSC-CANARY`：MSE金丝雀发布。 |
|Sign|String|否|a9f8\*\*\*\*|场景编码，明确知道目标业务场景编码时设置。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ArmsScenarios|Array of ArmsScenarios| |业务监控详细信息。 |
|AppId|String|b590lhguqs@28f515462\*\*\*\*\*\*|应用ID。 |
|CreateTime|String|1585214916000|业务监控创建时间。 |
|Extensions|String|\{"\_MODE": "CUSTOM-TRANSACTION","\_SCENARIO": "USER-DEFINED"\}|扩展信息字段JSON串。 |
|Id|Long|132|业务监控ID。 |
|Name|String|测试业务监控|业务监控名称。 |
|RegionId|String|cn-zhangjiakou|地域ID。 |
|Sign|String|a9f8\*\*\*\*|业务监控对应编码。 |
|UpdateTime|String|1585214916000|业务监控更新时间。 |
|UserId|String|113197164949\*\*\*\*|用户ID。 |
|RequestId|String|98027D1F-3AEB-492C-A4AA-E9217992\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListScenario
&AppId=b590lhguqs@28f515462******
&Name=测试业务监控
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListScenarioResponse>
  <RequestId>98027D1F-3AEB-492C-A4AA-E9217992****</RequestId>
  <ArmsScenarios>
        <AppId>b590lhguqs@28f515462******</AppId>
        <UserId>113197164949****</UserId>
        <CreateTime>1585214916000</CreateTime>
        <UpdateTime>1585214916000</UpdateTime>
        <Sign>a9f8****</Sign>
        <RegionId>cn-zhangjiakou</RegionId>
        <Id>132</Id>
        <Extensions>{"_MODE": "CUSTOM-TRANSACTION","_SCENARIO": "USER-DEFINED"}</Extensions>
        <Name>测试业务监控</Name>
  </ArmsScenarios>
</ListScenarioResponse>
```

`JSON`格式

```
{
    "RequestId": "98027D1F-3AEB-492C-A4AA-E9217992****",
    "ArmsScenarios": {
        "AppId": "b590lhguqs@28f515462******",
        "UserId": "113197164949****",
        "CreateTime": 1585214916000,
        "UpdateTime": 1585214916000,
        "Sign": "a9f8****",
        "RegionId": "cn-zhangjiakou",
        "Id": 132,
        "Extensions": "{\"_MODE\": \"CUSTOM-TRANSACTION\",\"_SCENARIO\": \"USER-DEFINED\"}",
        "Name": "测试业务监控"
    }
}
```

