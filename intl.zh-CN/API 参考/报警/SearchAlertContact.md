# SearchAlertContact {#doc_api_ARMS_SearchAlertContact .reference}

调用 SearchAlertContact 查询报警联系人。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertContact|系统规定参数，取值为 `SearchAlertContact`。

 |
|ContactName|String|是|JohnDoe|联系人姓名

 |
|CurrentPage|String|是|1|当前查询页码

 |
|Email|String|是|johndoe@example.com|邮箱

 |
|PageSize|String|是|5|页面数据行数

 |
|Phone|String|是|12312312312|电话号码

 |
|RegionId|String|是|cn-hangzhou|地域 ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean| | |每页返回信息

 |
|Contacts| | |联系人信息

 |
|ContactId|Long|6258|报警联系人 ID

 |
|ContactName|String|JohnDoe|报警联系人姓名

 |
|CreateTime|Long|1565671490000|创建时间

 |
|DingRobot|String|123456|钉钉机器人地址

 |
|Email|String|johndoe@example.com|邮箱

 |
|Phone|String|1381111\*\*\*\*|电话号码

 |
|SystemNoc|Boolean|false|是否同步系统信息

 |
|UpdateTime|Long|1565671490000|更新时间

 |
|UserId|String|xxxxxxxxxxxxx|用户 ID

 |
|PageNumber|Integer|1|当前查询页

 |
|PageSize|Integer|10|页面包含数据大小

 |
|TotalCount|Integer|2|查询总计

 |
|RequestId|String|6D01BD42-26B6-4C12-8AEF-1ACE9CBD2A39|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/SearchAlertContact.json?ContactName=JohnDoe
&CurrentPage=1
&Email=johndoe@example.com
&PageSize=5
&Phone=12312312312
&RegionId=cn-hangzhou

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<o>
       <pageBean class="object">
              <contacts class="array">
                     <e class="object">
                            <contactId type="number">6258</contactId>
                            <contactName type="string">JohnDoe</contactName>
                            <createTime type="number">1565671490000</createTime>
                            <dingRobot type="string"></dingRobot>
                            <email type="string"></email>
                            <phone type="string">1381111****</phone>
                            <systemNoc type="boolean">false</systemNoc>
                            <updateTime type="number">1565671490000</updateTime>
                            <userId type="string">xxxxxxxxxxxxx</userId>
                     </e>
                     <e class="object">
                            <contactId type="number">6259</contactId>
                            <contactName type="string">JaneDoe</contactName>
                            <createTime type="number">1565671814000</createTime>
                            <dingRobot type="string"></dingRobot>
                            <email type="string"></email>
                            <phone type="string">1382222****</phone>
                            <systemNoc type="boolean">false</systemNoc>
                            <updateTime type="number">1565671814000</updateTime>
                            <userId type="string">xxxxxxxxxxxxx</userId>
                     </e>
              </contacts>
              <pageNumber type="number">1</pageNumber>
              <pageSize type="number">10</pageSize>
              <totalCount type="number">2</totalCount>
       </pageBean>
       <requestId type="string">6D01BD42-26B6-4C12-8AEF-1ACE9CBD2A39</requestId>
</o>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"pageBean":{
		"totalCount":2,
		"pageSize":10,
		"pageNumber":1,
		"contacts":[
			{
				"createTime":1565671490000,
				"phone":"1381111****",
				"contactId":6258,
				"dingRobot":"",
				"updateTime":1565671490000,
				"email":"",
				"contactName":"JohnDoe",
				"userId":"xxxxxxxxxxxxx",
				"systemNoc":false
			},
			{
				"createTime":1565671814000,
				"phone":"1382222****",
				"contactId":6259,
				"dingRobot":"",
				"updateTime":1565671814000,
				"email":"",
				"contactName":"JaneDoe",
				"userId":"xxxxxxxxxxxxx",
				"systemNoc":false
			}
		]
	},
	"requestId":"6D01BD42-26B6-4C12-8AEF-1ACE9CBD2A39"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/ARMS)查看更多错误码。

