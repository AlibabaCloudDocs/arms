# SearchRetcodeAppByPage

You can call this operation to query browser monitoring jobs by page.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchRetcodeAppByPage|The operation that you want to perform. Set this value to `SearchRetcodeAppByPage`. |
|PageNumber|Integer|Yes|1|The number of the page to return. |
|PageSize|Integer|Yes|5|The number of entries to return on each page. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|Yes|App1|The name of the application monitored. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean| | |The information returned on each page. |
|PageNumber|Integer|1|The number of the page returned. |
|PageSize|Integer|2|The number of entries returned on each page. |
|RetcodeApps| | |The browser monitoring job information returned on each page. |
|AppId|Long|16064|The ID of the application monitored. |
|AppName|String|a3|The name of the application monitored. |
|CreateTime|Long|1545363321000|The time when the browser monitoring job was created. |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|The PID. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Type|String|RETCODE|The monitoring type. |
|UpdateTime|Long|1545363321000|The time when the browser monitoring job was updated. |
|UserId|String|xxxxxxxxxxxxxx|The ID of the user. |
|TotalCount|Integer|8|The total number of entries returned. |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/SearchRetcodeAppByPage.json?PageNumber=1
&PageSize=5
&RegionId=cn-hangzhou
&RetcodeAppName=App1

```

Sample success response

`XML` format

```
<SearchRetcodeAppByPage>
       <requestId>626037F5-FDEB-45B0-804C-B3C92797A64E</requestId>
       <pageBean>
              <pageNumber>1</pageNumber>
              <pageSize>2</pageSize>
              <totalCount>8</totalCount>
              <retcodeApps>
                     <retcodeApp>
                            <appId>16064</appId>
                            <appName>a3</appName>
                            <createTime>1545363321000</createTime>
                            <pid>xxxxxxxxxxxxxxxxx</pid>
                            <regionId>cn-hangzhou</regionId>
                            <type>RETCODE</type>
                            <updateTime>1545363321000</updateTime>
                            <userId>xxxxxxxxxxxxxx</userId>
                     </retcodeApp>
                     <retcodeApp>
                            <appId>38093</appId>
                            <appName>TestApp</appName>
                            <createTime>1553239261000</createTime>
                            <pid>xxxxxxxxxxxxxxxxxxxxxxxxx</pid>
                            <regionId>cn-hangzhou</regionId>
                            <type>RETCODE</type>
                            <updateTime>1553239261000</updateTime>
                            <userId>xxxxxxxxxxxx</userId>
                     </retcodeApp>
              </retcodeApps>
       </pageBean>
</SearchRetcodeAppByPage>
```

`JSON` format

```
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

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

