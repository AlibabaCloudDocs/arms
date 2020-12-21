# DeleteRetcodeApp

调用 DeleteRetcodeApp 删除前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteRetcodeApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteRetcodeApp|系统规定参数，取值为 `DeleteRetcodeApp`。 |
|AppId|String|是|1231|应用 ID |
|RegionId|String|是|cn-hangzhou|地域 ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|true|删除成功或失败 |
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|请求 ID |

## 示例

请求示例

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/DeleteRetcodeApp.json?AppId=1231
&RegionId=cn-hangzhou

```

正常返回示例

`XML` 格式

```
<o>
       <data type="string">true</data>
       <requestId type="string">01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
</o>
```

`JSON` 格式

```
{
	"requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
	"data":"true"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ARMS)查看更多错误码。

