# ListRetcodeApps {#doc_api_ARMS_ListRetcodeApps .reference}

调用 ListRetcodeApps 列出指定地域下全部前端监控任务。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ListRetcodeApps&type=RPC&version=2019-08-08)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListRetcodeApps|系统规定参数，取值为 `ListRetcodeApps`。

 |
|RegionId|String|是|cn-hangzhou|地域 ID

 |
|AccessKeyId|String|否|\*\*\*\*|忽略

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|99A663CB-8D7B-4B0D-A006-03C8EE38E7BB|请求 ID

 |
|RetcodeApps| | |前端监控应用列表信息

 |
|AppId|Long|16064|应用 ID

 |
|AppName|String|a3|应用名称

 |
|Pid|String|xxxxxxxxxxxxxxxxx|PID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/ListRetcodeApps.json?RegionId=cn-hangzhou

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<o>
       <requestId type="string">99A663CB-8D7B-4B0D-A006-03C8EE38E7BB</requestId>
       <retcodeApps class="array">
              <e class="object">
                     <appId type="number">16064</appId>
                     <appName type="string">a3</appName>
                     <pid type="string">xxxxxxxxxxxxxxxxx</pid>
              </e>
              <e class="object">
                     <appId type="number">38093</appId>
                     <appName type="string">ARMS页面</appName>
                     <pid type="string">xxxxxxxxxxxxxxxxxxxxx</pid>
              </e>
              <e class="object">
                     <appId type="number">77494</appId>
                     <appName type="string">ARMS-Retcode页面</appName>
                     <pid type="string">xxxxxxxxxxxxxxxxxxxxxxx</pid>
              </e>
              <e class="object">
                     <appId type="number">77499</appId>
                     <appName type="string">测试1</appName>
                     <pid type="string">xxxxxxxxxxxxxxxxxxxxxx</pid>
              </e>
              <e class="object">
                     <appId type="number">77501</appId>
                     <appName type="string">前端测试</appName>
                     <pid type="string">xxxxxxxxxxxxxxxxxx</pid>
              </e>
       </retcodeApps>
</o>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"99A663CB-8D7B-4B0D-A006-03C8EE38E7BB",
	"retcodeApps":[
		{
			"appName":"a3",
			"appId":16064,
			"pid":"xxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"ARMS页面",
			"appId":38093,
			"pid":"xxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"ARMS-Retcode页面",
			"appId":77494,
			"pid":"xxxxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"测试1",
			"appId":77499,
			"pid":"xxxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"前端测试",
			"appId":77501,
			"pid":"xxxxxxxxxxxxxxxxxx"
		}
	]
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ARMS)查看更多错误码。

