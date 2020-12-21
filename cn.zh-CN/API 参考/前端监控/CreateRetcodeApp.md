# CreateRetcodeApp

调用 CreateRetcodeApp 创建前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=CreateRetcodeApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。 |
|RetcodeAppName|String|是|SdkTest|前端监控应用名称。 |
|RetcodeAppType|String|是|web|前端监控应用类型，包括 web、weex、mini\_dd、mini\_alipay、mini\_wx 和 mini\_common。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|请求 ID。 |
|RetcodeAppDataBean|Struct| |返回前端监控创建信息。 |
|AppId|Long|135143|应用 ID。 |
|Pid|String|aokcdqn3ly@a195c6d6421\*\*\*\*|PID。 |

## 示例

请求示例

```
http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/CreateRetcodeApp.json?RegionId=cn-hangzhou
&RetcodeAppName=SdkTest
&RetcodeAppType=web
```

正常返回示例

`XML` 格式

```
<CreateRetcodeApp>
       <requestId>A5EC8221-08F2-4C95-9AF1-49FD998C647A</requestId>
       <retcodeAppDataBean>
              <appId>135143</appId>
              <pid>aokcdqn3ly@a195c6d6421****</pid>
       </retcodeAppDataBean>
</CreateRetcodeApp>
```

`JSON` 格式

```
{
    "requestId": "A5EC8221-08F2-4C95-9AF1-49FD998C647A",
    "retcodeAppDataBean": {
        "appId": 135143,
        "pid": "aokcdqn3ly@a195c6d6421****"
    }
}
```

