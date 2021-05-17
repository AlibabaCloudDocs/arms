# ListRetcodeApps

Queries all frontend monitoring tasks in a specified region.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListRetcodeApps&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListRetcodeApps|The operation that you want to perform. Set the value to **ListRetcodeApps**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|99A663CB-8D7B-4B0D-A006-03C8EE38E7BB|The ID of the request. |
|RetcodeApps|Array of RetcodeApp| |The information about monitored applications. |
|AppId|Long|16064|The ID of the application. It is an auto-increment parameter of the database. |
|AppName|String|a3|The name of the application. |
|Pid|String|atc889zkcf@d8deedfa9bf\*\*\*\*|The process identifier \(PID\) of the application. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=ListRetcodeApps
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListRetcodeAppsResponse>
  <RequestId>99A663CB-8D7B-4B0D-A006-03C8EE38E7BB</RequestId>
  <RetcodeApps>
        <Pid>atc889zkcf@d8deedfa9bf****</Pid>
        <AppId>16064</AppId>
        <AppName>a3</AppName>
  </RetcodeApps>
</ListRetcodeAppsResponse>
```

`JSON` format

```
{
    "RequestId": "99A663CB-8D7B-4B0D-A006-03C8EE38E7BB",
    "RetcodeApps": {
        "Pid": "atc889zkcf@d8deedfa9bf****",
        "AppId": 16064,
        "AppName": "a3"
    }
}
```

