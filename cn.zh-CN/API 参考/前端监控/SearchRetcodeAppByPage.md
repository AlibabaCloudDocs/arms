# SearchRetcodeAppByPage {#doc_api_ARMS_SearchRetcodeAppByPage .reference}

调用 SearchRetcodeAppByPage 分页查询前端监控任务。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchRetcodeAppByPage|系统规定参数，取值为 `SearchRetcodeAppByPage`。

 |
|PageNumber|Integer|是|1|当前查询页码

 |
|PageSize|Integer|是|5|每页数据行数

 |
|RegionId|String|是|cn-hangzhou|地域 ID

 |
|RetcodeAppName|String|是|App1|前端监控应用名称

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean| | |每页返回信息

 |
|PageNumber|Integer|1|当前查询页码

 |
|PageSize|Integer|2|每页数据行数

 |
|RetcodeApps| | |每页返回前端监控任务信息

 |
|AppId|Long|16064|应用 ID

 |
|AppName|String|a3|应用名称

 |
|CreateTime|Long|1545363321000|创建时间

 |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|PID

 |
|RegionId|String|cn-hangzhou|地域 ID

 |
|Type|String|RETCODE|监控类型

 |
|UpdateTime|Long|1545363321000|更新时间

 |
|UserId|String|xxxxxxxxxxxxxx|用户 ID

 |
|TotalCount|Integer|8|查询结果总数

 |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/SearchRetcodeAppByPage.json?PageNumber=1
&PageSize=5
&RegionId=cn-hangzhou
&RetcodeAppName=App1

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<o>
       <pageBean class="object">
              <pageNumber type="number">1</pageNumber>
              <pageSize type="number">2</pageSize>
              <retcodeApps class="array">
                     <e class="object">
                            <appId type="number">16064</appId>
                            <appName type="string">a3</appName>
                            <createTime type="number">1545363321000</createTime>
                            <pid type="string">xxxxxxxxxxxxxxxxx</pid>
                            <regionId type="string">cn-hangzhou</regionId>
                            <type type="string">RETCODE</type>
                            <updateTime type="number">1545363321000</updateTime>
                            <userId type="string">xxxxxxxxxxxxxx</userId>
                     </e>
                     <e class="object">
                            <appId type="number">38093</appId>
                            <appName type="string">TestApp</appName>
                            <createTime type="number">1553239261000</createTime>
                            <pid type="string">xxxxxxxxxxxxxxxxxxxxxxxxx</pid>
                            <regionId type="string">cn-hangzhou</regionId>
                            <type type="string">RETCODE</type>
                            <updateTime type="number">1553239261000</updateTime>
                            <userId type="string">xxxxxxxxxxxx</userId>
                     </e>
              </retcodeApps>
              <totalCount type="number">8</totalCount>
       </pageBean>
       <requestId type="string">626037F5-FDEB-45B0-804C-B3C92797A64E</requestId>
</o>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"pageBean":{
		"totalCount":8,
		"pageSize":2,
		"pageNumber":1,
		"retcodeApps":[
			{
				"appName":"a3",
				"createTime":1545363321000,
				"appId":16064,
				"updateTime":1545363321000,
				"userId":"xxxxxxxxxxxxxx",
				"pid":"xxxxxxxxxxxxxxxxx",
				"type":"RETCODE",
				"regionId":"cn-hangzhou"
			},
			{
				"appName":"TestApp",
				"createTime":1553239261000,
				"appId":38093,
				"updateTime":1553239261000,
				"userId":"xxxxxxxxxxxx",
				"pid":"xxxxxxxxxxxxxxxxxxxxxxxxx",
				"type":"RETCODE",
				"regionId":"cn-hangzhou"
			}
		]
	},
	"requestId":"626037F5-FDEB-45B0-804C-B3C92797A64E"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/ARMS)查看更多错误码。

