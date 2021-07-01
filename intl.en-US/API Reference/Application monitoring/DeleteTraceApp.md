# DeleteTraceApp

Deletes an application based on a specified process identifier \(PID\) and type.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DeleteTraceApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteTraceApp|The operation that you want to perform. Set the value to `DeleteTraceApp`. |
|Pid|String|Yes|9w0sc5gxxz@edcsd447c2f\*\*\*\*|The PID of the application that you want to delete. For more information about how to obtain the PID, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Type|String|Yes|TRACE|The type of the application that you want to delete. You can call the SearchTraceAppByName operation to query the application type. For more information, see [SearchTraceAppByName](~~130676~~). Valid values:

-   `TRACE`: application monitoring
-   `RETCODE`: frontend monitoring |
|AppId|String|No|5406\*\*|The ID of the application that you want to delete. You can call the SearchTraceAppByName operation to query the application ID. For more information, see [SearchTraceAppByName](~~130676~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|\{ "RequestId": "46355DD8-FC56-40C5-BFC6-269DE4F9\*\*\*\*", "Data": "\{\\"code\\":200,\\"data\\":\\"\{\\\\\\"code\\\\\\":200,\\\\\\"data\\\\\\":true,\\\\\\"errorCode\\\\\\":\\\\\\"The application is deleted\\\\\\",\\\\\\"message\\\\\\":\\\\\\"The application is deleted\\\\\\",\\\\\\"success\\\\\\":true,\\\\\\"traceId\\\\\\":\\\\\\"0bc0594d15954826692915817e\*\*\*\*\\\\\\"\}\\",\\"errorCode\\":\\"The application is deleted\\",\\"message\\":\\"The application is deleted\\",\\"success\\":true,\\"traceId\\":\\"0ab2646915954826692568137d\*\*\*\*\\"\}" \}|The response in JSON format, including the HTTP status code, error code, response message, and trace ID. |
|RequestId|String|46355DD8-FC56-40C5-BFC6-269DE4F9\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DeleteTraceApp
&Pid=9w0sc5gxxz@edcsd447c2f****
&RegionId=cn-hangzhou
&Type=TRACE
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteTraceAppResponse>
      <RequestId>46355DD8-FC56-40C5-BFC6-269DE4F9****</RequestId>
      <Data>{"code":200,"data":"{\"code\":200,\"data\":true,\"errorCode\":\"The application is deleted\",\"message\":\"The application is deleted\",\"success\":true,\"traceId\":\"0bc0594d15954826692915817e****\"}","errorCode":"The application is deleted","message":"The application is deleted","success":true,"traceId":"0ab2646915954826692568137d****"}</Data>
</DeleteTraceAppResponse>
```

`JSON` format

```
{"RequestId":"46355DD8-FC56-40C5-BFC6-269DE4F9****","Data":"{ \t\"RequestId\": \"46355DD8-FC56-40C5-BFC6-269DE4F9****\", \t\"Data\": \"{\\\"code\\\":200,\\\"data\\\":\\\"{\\\\\\\"code\\\\\\\":200,\\\\\\\"data\\\\\\\":true,\\\\\\\"errorCode\\\\\\\":\\\\\\\"The application is deleted\\\\\\\",\\\\\\\"message\\\\\\\":\\\\\\\"The application is deleted\\\\\\\",\\\\\\\"success\\\\\\\":true,\\\\\\\"traceId\\\\\\\":\\\\\\\"0bc0594d15954826692915817e****\\\\\\\"}\\\",\\\"errorCode\\\":\\\"The application is deleted\\\",\\\"message\\\":\\\"The application is deleted\\\",\\\"success\\\":true,\\\"traceId\\\":\\\"0ab2646915954826692568137d****\\\"}\" }"}
```

