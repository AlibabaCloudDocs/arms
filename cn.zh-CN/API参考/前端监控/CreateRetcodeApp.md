# CreateRetcodeApp

调用CreateRetcodeApp创建前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=CreateRetcodeApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateRetcodeApp|系统规定参数。取值：CreateRetcodeApp。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|RetcodeAppName|String|是|SdkTest|前端监控应用名称。 |
|RetcodeAppType|String|是|mini\_dd|前端监控应用类型，包括`web`、`weex`、`mini_dd`、`mini_alipay`、`mini_wx`和`mini_common`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|请求ID。 |
|RetcodeAppDataBean|Struct| |返回前端监控创建信息。 |
|AppId|Long|135143|应用ID。 |
|Pid|String|aokcdqn3ly@a195c6d6421\*\*\*\*|PID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateRetcodeApp
&RegionId=cn-hangzhou
&RetcodeAppName=SdkTest
&RetcodeAppType=mini_dd
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateRetcodeAppResponse>
      <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C647A</RequestId>
      <RetcodeAppDataBean>
            <AppId>135143</AppId>
            <Pid>aokcdqn3ly@a195c6d6421****</Pid>
      </RetcodeAppDataBean>
</CreateRetcodeAppResponse>
```

`JSON`格式

```
{
    "RequestId": "A5EC8221-08F2-4C95-9AF1-49FD998C647A",
    "RetcodeAppDataBean": {
        "AppId": 135143,
        "Pid": "aokcdqn3ly@a195c6d6421****"
    }
}
```

