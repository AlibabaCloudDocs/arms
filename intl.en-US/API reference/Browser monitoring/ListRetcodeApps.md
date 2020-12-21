# ListRetcodeApps

Queries all browser monitoring tasks in a specified region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListRetcodeApps&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListRetcodeApps|The operation that you want to perform. Set the value to `ListRetcodeApps`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|AccessKeyId|String|No|\*\*\*\*|You do not need to specify this parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|99A663CB-8D7B-4B0D-A006-03C8EE38E7BB|The ID of the request. |
|RetcodeApps| | |The list of monitored applications. |
|AppId|Long|16064|The ID of the application. |
|AppName|String|a3|The name of the application. |
|Pid|String|xxxxxxxxxxxxxxxxx|PID |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/ListRetcodeApps.json?RegionId=cn-hangzhou

```

Sample success responses

`XML` format

```
<ListRetcodeApps>
       <RequestId>99A663CB-8D7B-4B0D-A006-03C8EE38E7BB</RequestId>
       <RetcodeApps>
              <RetcodeApp>
                     <AppId>16064</AppId>
                     <AppName>a3</AppName>
                     <Pid>xxxxxxxxxxxxxxxxx</Pid>
              </RetcodeApp>
              <RetcodeApp>
                     <AppId>38093</AppId>
                     <AppName>ARMS page</AppName>
                     <Pid>xxxxxxxxxxxxxxxxxxxxx</Pid>
              </RetcodeApp>
              <RetcodeApp>
                     <AppId>77494</AppId>
                     <AppName>ARMS-Retcode page</AppName>
                     <Pid>xxxxxxxxxxxxxxxxxxxxxxx</Pid>
              </RetcodeApp>
              <RetcodeApp>
                     <AppId>77499</AppId>
                     <AppName>Test 1</AppName>
                     <Pid>xxxxxxxxxxxxxxxxxxxxxx</Pid>
              </RetcodeApp>
              <RetcodeApp>
                     <AppId>77501</AppId>
                     <AppName>Browser monitoring</AppName>
                     <Pid>xxxxxxxxxxxxxxxxxx</Pid>
              </RetcodeApp>
       </RetcodeApps>
</ListRetcodeApps>
```

`JSON` format

```
{
	"requestId":"99A663CB-8D7B-4B0D-A006-03C8EE38E7BB",
	"retcodeApps":[
		{
			"appName":"a3",
			"appId":16064,
			"pid":"xxxxxxxxxxxxxxxxx"
		},
		{
			"appName": "ARMS page",
			"appId":38093,
			"pid":"xxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"ARMS-Retcode page",
			"appId":77494,
			"pid":"xxxxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"Test 1",
			"appId":77499,
			"pid":"xxxxxxxxxxxxxxxxxxxxxx"
		},
		{
			"appName":"Browser monitoring",
			"appId":77501,
			"pid":"xxxxxxxxxxxxxxxxxx"
		}
	]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

