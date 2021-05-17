# GetTraceApp

Queries the details of an application monitoring task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetTraceApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTraceApp|The operation that you want to perform. Set the value to `GetTraceApp`. |
|Pid|String|Yes|atc889zkcf@d8deedfa9bfxxxx|The process identifier \(PID\) of the application. For more information, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|CBFA2436-9453-4991-AC0E-9DC42A26\*\*\*\*|The ID of the request. |
|TraceApp|Struct| |The struct returned. |
|AppId|Long|123|The ID of the application. |
|AppName|String|test-app|The name of the application. |
|CreateTime|Long|1529667762000|The timestamp when the application was created. |
|Labels|List|prod|The tag of the application. |
|Pid|String|atc889zkcf@d8deedfa9bfxxxx|The PID of the application. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|Show|Boolean|true|Indicates whether the application is displayed in the Application Real-Time Monitoring Service \(ARMS\) console. Valid values:

 -   `true`: The application is displayed in the ARMS console.
-   `false`: The application is not displayed in the ARMS console. |
|Type|String|TRACE|The type of the monitoring task. Valid values:

 -   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|UpdateTime|Long|1529667762000|The timestamp when the task was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetTraceApp
&Pid=atc889zkcf@d8deedfa9bfxxxx
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetTraceAppResponse>
	  <RequestId>CBFA2436-9453-4991-AC0E-9DC42A26****</RequestId>
	  <TraceApp>
		    <Type>TRACE</Type>
		    <AppId>123</AppId>
		    <UserId>113197164949****</UserId>
		    <CreateTime>1529667762000</CreateTime>
		    <UpdateTime>1529667762000</UpdateTime>
		    <Pid>atc889zkcf@d8deedfa9bfxxxx</Pid>
		    <Show>true</Show>
		    <Labels>prod</Labels>
		    <RegionId>cn-hangzhou</RegionId>
		    <AppName>test-app</AppName>
	  </TraceApp>
</GetTraceAppResponse>
```

`JSON` format

```
{
    "RequestId": "CBFA2436-9453-4991-AC0E-9DC42A26****",
    "TraceApp": {
        "Type": "TRACE",
        "AppId": 123,
        "UserId": "113197164949****",
        "CreateTime": 1529667762000,
        "UpdateTime": 1529667762000,
        "Pid": "atc889zkcf@d8deedfa9bfxxxx",
        "Show": true,
        "Labels": "prod",
        "RegionId": "cn-hangzhou",
        "AppName": "test-app"
    }
}
```

