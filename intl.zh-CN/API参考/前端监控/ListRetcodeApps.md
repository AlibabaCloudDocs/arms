# ListRetcodeApps

调用ListRetcodeApps接口列出指定地域下全部前端监控任务。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListRetcodeApps&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListRetcodeApps|系统规定参数。取值：**ListRetcodeApps**。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|99A663CB-8D7B-4B0D-A006-03C8EE38E7BB|请求ID。 |
|RetcodeApps|Array of RetcodeApp| |前端监控应用列表信息。 |
|AppId|Long|16064|应用ID，数据库自增字段。 |
|AppName|String|A1|前端应用名称。 |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|应用的ID标识串。 |
|RetcodeAppType|String|web|接入的前端类型。

 -   `web`：Web端。
-   `weex`：Weex端。
-   `mini_dd`：钉钉E应用。
-   `mini_alipay`：支付宝小程序。
-   `mini_wx`：微信小程序。
-   `mini_common`：其他类型小程序。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListRetcodeApps
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListRetcodeAppsResponse>
  <RequestId>99A663CB-8D7B-4B0D-A006-03C8EE38E7BB</RequestId>
  <RetcodeApps>
        <RetcodeAppType>web</RetcodeAppType>
        <AppId>16064</AppId>
        <Pid>atc889zkcf@d8deedfa9bf****</Pid>
        <AppName>A1</AppName>
  </RetcodeApps>
</ListRetcodeAppsResponse>
```

`JSON`格式

```
{
    "RequestId": "99A663CB-8D7B-4B0D-A006-03C8EE38E7BB",
    "RetcodeApps": {
        "RetcodeAppType": "web",
        "AppId": 16064,
        "Pid": "atc889zkcf@d8deedfa9bf****",
        "AppName": "A1"
    }
}
```

