# SearchRetcodeAppByPage

Queries frontend monitoring jobs for applications by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SearchRetcodeAppByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchRetcodeAppByPage|The operation that you want to perform. Set the value to SearchRetcodeAppByPage. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|No|App1|The name of the application that is monitored by the frontend monitoring feature. |
|PageNumber|Integer|No|1|The number of the page to return. |
|PageSize|Integer|No|5|The number of entries to return on each page. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageBean|Struct| |The information returned on the current page. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|2|The number of entries returned per page. |
|RetcodeApps|Array of RetcodeApp| |The information about the frontend monitoring job. |
|AppId|Long|16064|The ID of the application. It is an auto-increment parameter of the database. |
|AppName|String|a3|The name of the application. |
|CreateTime|Long|1545363321000|The timestamp when the application was created. |
|Pid|String|aokcdqn3ly@741623b4e91\*\*\*\*|The process identifier \(PID\) of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Type|String|RETCODE|The type of the monitoring job. Valid values:

-   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|UpdateTime|Long|1545363321000|The timestamp when the application was updated. |
|UserId|String|12341234|The ID of the user. |
|TotalCount|Integer|8|The total number of entries returned. |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797A64E|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SearchRetcodeAppByPage
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

