# CreateRetcodeApp

You can call this operation to create a browser monitoring job.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=CreateRetcodeApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateRetcodeApp|The operation that you want to perform. Set this value to `CreateRetcodeApp`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|RetcodeAppName|String|Yes|SdkTest|The name of the application for which you want to create the browser monitoring job. |
|RetcodeAppType|String|Yes|web|The type of the application for which you want to create the browser monitoring job. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|The ID of the request. |
|RetcodeAppDataBean| | |The returned creation information of the browser monitoring job. |
|AppId|Long|135143|The ID of the application for which you created the browser monitoring job. |
|Pid|String|aokcdqn3ly@a195c6d6421\*\*\*\*|The PID. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/CreateRetcodeApp.json?RegionId=cn-hangzhou
&RetcodeAppName=SdkTest
&RetcodeAppType=web

```

Sample success response

`XML` format

```
<o>
       <requestId type="string">A5EC8221-08F2-4C95-9AF1-49FD998C647A</requestId>
       <retcodeAppDataBean class="object">
              <appId type="number">135143</appId>
              <pid type="string">aokcdqn3ly@a195c6d6421****</pid>
       </retcodeAppDataBean>
</o>
```

`JSON` format

```
{
	"requestId":"A5EC8221-08F2-4C95-9AF1-49FD998C647A",
	"retcodeAppDataBean":{
		"appId":135143,
		"pid":"aokcdqn3ly@a195c6d6421****"
	}
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

