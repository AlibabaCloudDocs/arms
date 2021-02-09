# DeleteRetcodeApp

调用DeleteRetcodeApp接口删除前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteRetcodeApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteRetcodeApp|系统规定参数，取值为 `DeleteRetcodeApp`。 |
|AppId|String|是|1231|应用ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|true|是否成功删除：

 -   `true`：删除成功。
-   `false`：删除失败。 |
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteRetcodeApp
&AppId=1231
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteRetcodeAppResponse>
       <data>true</data>
       <requestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
</DeleteRetcodeAppResponse>
```

`JSON`格式

```
{
    "requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
    "data":"true"
}
```

