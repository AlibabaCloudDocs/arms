# SearchRetcodeAppByPage

Queries browser monitoring jobs for applications by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|PageNumber|Integer|Yes|1|The number of the page to return. |
|PageSize|Integer|Yes|5|The number of entries to return on each page. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|Yes|App1|The name of the application that is monitored by Browser Monitoring. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|The ID of the request. |
|PageBean|Struct| |The information returned on each page. |
|TotalCount|Integer|8|The total number of entries returned. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|2|The number of entries returned per page. |
|RetcodeApps|Array| |The browser monitoring job information returned per page. |
|AppId|Long|16064|The ID of the application. It is an auto-increment field of the database. |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|The string of the application ID. |
|AppName|String|a3|The name of the application. |
|Type|String|RETCODE|The type of the monitoring job. Valid values: **TRACE:** application monitoring. **RETCODE:** browser monitoring. |
|UserId|String|12341234|The ID of the user. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|CreateTime|Long|1545363321000|The time when the monitoring job was created. |
|UpdateTime|Long|1545363321000|The time when the monitoring job was updated. |

## Examples

Sample requests

```
http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/SearchRetcodeAppByPage.json?PageNumber=1
&PageSize=5
&RegionId=cn-hangzhou
&RetcodeAppName=App1
```

Sample success responses

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
    "requestId": "626037F5-FDEB-45B0-804C-B3C92797A64E",
    "pageBean": {
        "totalCount": 8,
        "pageNumber": 1,
        "pageSize": 2,
        "retcodeApps": [
            {
                "appId": 16064,
                "pid": "xxxxxxxxxxxxxxxxx",
                "appName": "a3",
                "type": "RETCODE",
                "userId": "xxxxxxxxxxxxxx",
                "regionId": "cn-hangzhou",
                "createTime": 1545363321000,
                "updateTime": 1545363321000
            },
            {
                "appId": 38093,
                "pid": "xxxxxxxxxxxxxxxxxxxxxxxxx",
                "appName": "TestApp",
                "type": "RETCODE",
                "userId": "xxxxxxxxxxxx",
                "regionId": "cn-hangzhou",
                "createTime": 1553239261000,
                "updateTime": 1553239261000
            }
        ]
    }
}
```

