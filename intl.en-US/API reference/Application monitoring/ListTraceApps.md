# ListTraceApps

You can call this operation to query all application monitoring jobs in the specified region.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=ListTraceApps&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTraceApps|The operation that you want to perform. Set this value to `ListTraceApps`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region that you want to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|Integer|200|The response code. |
|Message|String|true|The information returned. |
|RequestId|String|959C77E2-04E9-4FD4-848A-B8C1A48BEF51|The ID of the request. |
|Success|Boolean|true|Indicates whether the request is successful. |
|TraceApps| | |The list of application monitoring jobs returned. |
|AppId|Long|5918|The ID of the application monitored. |
|AppName|String|arms-pop-hz|The name of the application monitored. |
|CreateTime|Long|1529667762000|The time when the application monitoring job was created. |
|Pid|String|xxxxxxxxxx|The PID. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Type|String|TRACE|The monitoring type. |
|UpdateTime|Long|1529667762000|The time when the application monitoring job was updated. |
|UserId|String|xxxxxxxxxxxxxxxx|The ID of the user. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/trace/ListTraceApps.json?Region=cn-hangzhou

```

Sample success response

`XML` format

```
<o>
       <requestId type="string">959C77E2-04E9-4FD4-848A-B8C1A48BEF51</requestId>
       <traceApps class="array">
              <e class="object">
                     <appId type="number">5918</appId>
                     <appName type="string">arms-pop-hz</appName>
                     <createTime type="number">1529667762000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1529667762000</updateTime>
                     <userId type="string">xxxxxxxxxxxxxxxx</userId>
              </e>
              <e class="object">
                     <appId type="number">6549</appId>
                     <appName type="string">docker-demo</appName>
                     <createTime type="number">1531291867000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1531291867000</updateTime>
                     <userId type="string">xxxxxxxxxxxxxxxx</userId>
              </e>
              <e class="object">
                     <appId type="number">7451</appId>
                     <appName type="string">arms-console-hz</appName>
                     <createTime type="number">1533525518000</createTime>
                     <pid type="string">xxxxxxxxxxxxxxxxxxx</pid>
                     <regionId type="string">cn-hangzhou</regionId>
                     <type type="string">TRACE</type>
                     <updateTime type="number">1533525518000</updateTime>
                     <userId type="string">xxxxxxxxxxxxxxxx</userId>
              </e>
       </traceApps>
</o>
```

`JSON` format

```
{
	"traceApps":[
		{
			"appName":"arms-pop-hz",
			"createTime":1529667762000,
			"appId":5918,
			"updateTime":1529667762000,
			"userId":"xxxxxxxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"docker-demo",
			"createTime":1531291867000,
			"appId":6549,
			"updateTime":1531291867000,
			"userId":"xxxxxxxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"arms-console-hz",
			"createTime":1533525518000,
			"appId":7451,
			"updateTime":1533525518000,
			"userId":"xxxxxxxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		}
	],
	"requestId":"959C77E2-04E9-4FD4-848A-B8C1A48BEF51"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

