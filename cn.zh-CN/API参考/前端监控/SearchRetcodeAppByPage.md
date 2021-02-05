# SearchRetcodeAppByPage

调用 SearchRetcodeAppByPage 分页查询前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|PageNumber|Integer|是|1|当前查询页码 |
|PageSize|Integer|是|5|每页数据行数 |
|RegionId|String|是|cn-hangzhou|地域 ID |
|RetcodeAppName|String|是|App1|前端监控应用名称 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|请求 ID |
|PageBean|Struct| |每页返回信息 |
|TotalCount|Integer|8|查询结果总数 |
|PageNumber|Integer|1|当前查询页码 |
|PageSize|Integer|2|每页数据行数 |
|RetcodeApps|Array| |每页返回前端监控任务信息 |
|AppId|Long|16064|应用 ID，数据库自增字段。 |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|应用的 ID 标识串 |
|AppName|String|a3|应用名称 |
|Type|String|RETCODE|监控类型。**TRACE** 为应用监控，**RETCODE** 为前端监控。 |
|UserId|String|12341234|用户 ID |
|RegionId|String|cn-hangzhou|地域 ID |
|CreateTime|Long|1545363321000|创建时间 |
|UpdateTime|Long|1545363321000|更新时间 |

## 示例

请求示例

```
http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/SearchRetcodeAppByPage.json?PageNumber=1
&PageSize=5
&RegionId=cn-hangzhou
&RetcodeAppName=App1
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

