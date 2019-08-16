# SearchTraceAppByName {#doc_api_ARMS_SearchTraceAppByName .reference}

调用 SearchTraceAppByName 查询应用监控任务列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByName&type=RPC&version=2019-08-08)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchTraceAppByName|系统规定参数，取值为 `SearchTraceAppByName`。

 |
|RegionId|String|是|cn-hangzhou|地域 ID

 |
|TraceAppName|String|是|demo|应用名称

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|514078F3-3DA0-4180-95A0-D8F300CB71D2|地域 ID

 |
|TraceApps| | |应用监控信息

 |
|AppId|Long|6549|应用 ID

 |
|AppName|String|3123-docker-demo|应用名称

 |
|CreateTime|Long|1531291867000|创建时间

 |
|Pid|String|xxxxxxxxxxxxxxxx|PID

 |
|RegionId|String|cn-hangzhou|地域 ID

 |
|Type|String|TRACE|监控类型

 |
|UpdateTime|Long|1531291867000|更新时间

 |
|UserId|String|xxxxxxxxxxx|用户 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://arms.cn-hangzhou.aliyun-inc.com:8099/trace/SearchTraceAppByName.json?RegionId=cn-hangzhou
&TraceAppName=demo

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<o>
       <requestId type="string">514078F3-3DA0-4180-95A0-D8F300CB71D2</requestId>
       <traceApps class="array">
              <e class="object">
                     <appId type="number">6549</appId>
                     <appName type="string">3123-docker-demo</appName>
                     <createTime type="number">1531291867000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1531291867000</updateTime>
                     <userId type="string">xxxxxxxxxxx</userId>
              </e>
              <e class="object">
                     <appId type="number">10198</appId>
                     <appName type="string">13312-demo</appName>
                     <createTime type="number">1540189384000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1540189384000</updateTime>
                     <userId type="string">xxxxxxxxxxx</userId>
              </e>
              <e class="object">
                     <appId type="number">128985</appId>
                     <appName type="string">dubboDemoConsumer</appName>
                     <createTime type="number">1565147950000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1565147950000</updateTime>
                     <userId type="string">xxxxxxxxxxxx</userId>
              </e>
       </traceApps>
</o>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"traceApps":[
		{
			"appName":"3123-docker-demo",
			"createTime":1531291867000,
			"appId":6549,
			"updateTime":1531291867000,
			"userId":"xxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"13312-demo",
			"createTime":1540189384000,
			"appId":10198,
			"updateTime":1540189384000,
			"userId":"xxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"dubboDemoConsumer",
			"createTime":1565147950000,
			"appId":128985,
			"updateTime":1565147950000,
			"userId":"xxxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		}
	],
	"requestId":"514078F3-3DA0-4180-95A0-D8F300CB71D2"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ARMS)查看更多错误码。

