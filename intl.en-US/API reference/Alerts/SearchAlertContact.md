# SearchAlertContact

You can call this operation to query alert contacts.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=SearchAlertContact&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertContact|The operation that you want to perform. Set this value to `SearchAlertContact`. |
|ContactName|String|Yes|JohnDoe|The name of the contact that you want to query. |
|CurrentPage|String|Yes|1|The number of the page to return. |
|Email|String|Yes|johndoe@example.com|The email address of the contact. |
|PageSize|String|Yes|5|The number of entries to return on each page. |
|Phone|String|Yes|12312312312|The phone number of the contact. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean| | |The information returned on each page. |
|Contacts| | |The information about the contact that you queried. |
|ContactId|Long|6258|The ID of the alert contact. |
|ContactName|String|JohnDoe|The name of the alert contact. |
|CreateTime|Long|1565671490000|The time when the contact was created. |
|DingRobot|String|123456|The DingTalk Chatbot address of the contact. |
|Email|String|johndoe@example.com|The email address of the contact. |
|Phone|String|1381111\*\*\*\*|The phone number of the contact. |
|SystemNoc|Boolean|false|Indicates whether system information has been synchronized. |
|UpdateTime|Long|1565671490000|The time when the contact was updated. |
|UserId|String|xxxxxxxxxxxxx|The ID of the user. |
|PageNumber|Integer|1|The number of the page returned. |
|PageSize|Integer|10|The number of entries returned on each page. |
|TotalCount|Integer|2|The total number of entries returned. |
|RequestId|String|6D01BD42-26B6-4C12-8AEF-1ACE9CBD2A39|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/SearchAlertContact.json?ContactName=JohnDoe
&CurrentPage=1
&Email=johndoe@example.com
&PageSize=5
&Phone=12312312312
&RegionId=cn-hangzhou

```

Sample success response

`XML` format

```
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

`JSON` format

```
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

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

