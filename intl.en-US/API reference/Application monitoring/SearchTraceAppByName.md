# SearchTraceAppByName

You can call this operation to query the application monitoring job list.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=SearchTraceAppByName&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchTraceAppByName|The operation that you want to perform. Set this value to `SearchTraceAppByName`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TraceAppName|String|Yes|demo|The name of the application for which you want query the application monitoring jobs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|514078F3-3DA0-4180-95A0-D8F300CB71D2|The ID of the region. |
|TraceApps| | |The application monitoring information returned. |
|AppId|Long|6549|The ID of the application monitored. |
|AppName|String|3123-docker-demo|The name of the application monitored. |
|CreateTime|Long|1531291867000|The time when the application monitoring job was created. |
|Pid|String|xxxxxxxxxxxxxxxx|The PID. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Type|String|TRACE|The monitoring type. |
|UpdateTime|Long|1531291867000|The time when the application monitoring job was updated. |
|UserId|String|xxxxxxxxxxx|The ID of the user. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/trace/SearchTraceAppByName.json?RegionId=cn-hangzhou
&TraceAppName=demo

```

Sample success response

`XML` format

```
<SearchTraceAppByName>
       <requestId>514078F3-3DA0-4180-95A0-D8F300CB71D2</requestId>
       <traceApps>
              <traceApp>
                     <appId>6549</appId>
                     <appName>3123-docker-demo</appName>
                     <createTime>1531291867000</createTime>
                     <pid>xxxxxxxxxxxxxxxxxxxxxx</pid>
                     <regionId>cn-hangzhou</regionId>
                     <type>TRACE</type>
                     <updateTime>1531291867000</updateTime>
                     <userId>xxxxxxxxxxx</userId>
              </traceApp>
              <traceApp>
                     <appId>10198</appId>
                     <appName>13312-demo</appName>
                     <createTime>1540189384000</createTime>
                     <pid>xxxxxxxxxxxxxxxx</pid>
                     <regionId>cn-hangzhou</regionId>
                     <type>tRACE</type>
                     <updateTime>1540189384000</updateTime>
                     <userId>xxxxxxxxxxx</userId>
              </traceApp>
              <traceApp>
                     <appId>128985</appId>
                     <appName>dubboDemoConsumer</appName>
                     <createTime>1565147950000</createTime>
                     <pid>xxxxxxxxxxxxxxxx</pid>
                     <regionId>cn-hangzhou</regionId>
                     <type>tRACE</type>
                     <updateTime>1565147950000</updateTime>
                     <userId>xxxxxxxxxxxx</userId>
              </traceApp>
       </traceApps>
</SearchTraceAppByName>
```

`JSON` format

```
{
	"traceApps":[
		{
			"appName":"3123-docker-demo",
			"createTime":1531291867000,
			"appId":6549,
			"updateTime":1531291867000,
			"userId":"xxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"13312-demo",
			"createTime":1540189384000,
			"appId":10198,
			"updateTime":1540189384000,
			"userId":"xxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		},
		{
			"appName":"dubboDemoConsumer",
			"createTime":1565147950000,
			"appId":128985,
			"updateTime":1565147950000,
			"userId":"xxxxxxxxxxxx",
			"pid":"xxxxxxxxxxxxxxxx",
			"type":"TRACE",
			"regionId":"cn-hangzhou"
		}
	],
	"requestId":"514078F3-3DA0-4180-95A0-D8F300CB71D2"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

