# SearchRetcodeAppByPage

调用SearchRetcodeAppByPage分页查询前端监控任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchRetcodeAppByPage|系统规定参数。取值：SearchRetcodeAppByPage。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|RetcodeAppName|String|否|App1|前端监控应用名称。 |
|PageNumber|Integer|否|1|当前查询页码。 |
|PageSize|Integer|否|5|每页数据行数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |每页返回信息。 |
|PageNumber|Integer|1|当前查询页码。 |
|PageSize|Integer|2|每页数据行数。 |
|RetcodeApps|Array of RetcodeApp| |每页返回前端监控任务信息。 |
|AppId|Long|16064|应用ID，数据库自增字段。 |
|AppName|String|a3|应用名称。 |
|CreateTime|Long|1545363321000|创建时间。 |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|应用的ID标识串。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|Type|String|RETCODE|监控类型。

 -   `TRACE`：应用监控。
-   `RETCODE`：前端监控。 |
|UpdateTime|Long|1545363321000|更新时间。 |
|UserId|String|12341234|用户ID。 |
|TotalCount|Integer|8|查询结果总数。 |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchRetcodeAppByPage
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchRetcodeAppByPageResponse>
  <PageBean>
        <TotalCount>8</TotalCount>
        <PageSize>2</PageSize>
        <PageNumber>1</PageNumber>
        <RetcodeApps>
              <Type>RETCODE</Type>
              <AppId>16064</AppId>
              <UserId>12341234</UserId>
              <CreateTime>1545363321000</CreateTime>
              <UpdateTime>1545363321000</UpdateTime>
              <Pid>aokcdqn3ly@741623b4e91****</Pid>
              <RegionId>cn-hangzhou</RegionId>
              <AppName>a3</AppName>
        </RetcodeApps>
  </PageBean>
  <RequestId>626037F5-FDEB-45B0-804C-B3C92797A64E</RequestId>
</SearchRetcodeAppByPageResponse>
```

`JSON`格式

```
{
    "PageBean": {
        "TotalCount": 8,
        "PageSize": 2,
        "PageNumber": 1,
        "RetcodeApps": {
            "Type": "RETCODE",
            "AppId": 16064,
            "UserId": 12341234,
            "CreateTime": 1545363321000,
            "UpdateTime": 1545363321000,
            "Pid": "aokcdqn3ly@741623b4e91****",
            "RegionId": "cn-hangzhou",
            "AppName": "a3"
        }
    },
    "RequestId": "626037F5-FDEB-45B0-804C-B3C92797A64E"
}
```

