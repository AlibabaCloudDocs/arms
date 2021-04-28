# DeleteTraceApp

调用DeleteTraceApp接口删除指定ID和类型的应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DeleteTraceApp&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteTraceApp|系统规定参数，取值为`DeleteTraceApp`。 |
|Pid|String|是|9w0sc5gxxz@edcsd447c2f\*\*\*\*|应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr)。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Type|String|是|TRACE|需要删除的应用的类型，可调用SearchTraceAppByName接口获取，更多信息，请参见[SearchTraceAppByName](~~130676~~)。包括以下类型：

 -   `TRACE`：应用监控
-   `RETCODE`：为前端监控。 |
|AppId|String|否|5406\*\*|需要删除的应用的ID，可调用SearchTraceAppByName接口获取，更多信息，请参见[SearchTraceAppByName](~~130676~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|\{ "RequestId": "46355DD8-FC56-40C5-BFC6-269DE4F9\*\*\*\*", "Data": "\{\\"code\\":200,\\"data\\":\\"\{\\\\\\"code\\\\\\":200,\\\\\\"data\\\\\\":true,\\\\\\"errorCode\\\\\\":\\\\\\"删除应用成功\\\\\\",\\\\\\"message\\\\\\":\\\\\\"删除应用成功\\\\\\",\\\\\\"success\\\\\\":true,\\\\\\"traceId\\\\\\":\\\\\\"0bc0594d15954826692915817e\*\*\*\*\\\\\\"\}\\",\\"errorCode\\":\\"删除应用成功\\",\\"message\\":\\"删除应用成功\\",\\"success\\":true,\\"traceId\\":\\"0ab2646915954826692568137d\*\*\*\*\\"\}" \}|JSON格式的返回结果，包含HTTP状态码、错误码、返回消息、TraceId等。 |
|RequestId|String|46355DD8-FC56-40C5-BFC6-269DE4F9\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteTraceApp
&Pid=9w0sc5gxxz@edcsd447c2f****
&RegionId=cn-hangzhou
&Type=TRACE
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteTraceAppResponse>
	  <RequestId>46355DD8-FC56-40C5-BFC6-269DE4F9****</RequestId>
	  <Data>{"code":200,"data":"{\"code\":200,\"data\":true,\"errorCode\":\"删除应用成功\",\"message\":\"删除应用成功\",\"success\":true,\"traceId\":\"0bc0594d15954826692915817e****\"}","errorCode":"删除应用成功","message":"删除应用成功","success":true,"traceId":"0ab2646915954826692568137d****"}</Data>
</DeleteTraceAppResponse>
```

`JSON`格式

```
{"RequestId":"46355DD8-FC56-40C5-BFC6-269DE4F9****","Data":"{ \t\"RequestId\": \"46355DD8-FC56-40C5-BFC6-269DE4F9****\", \t\"Data\": \"{\\\"code\\\":200,\\\"data\\\":\\\"{\\\\\\\"code\\\\\\\":200,\\\\\\\"data\\\\\\\":true,\\\\\\\"errorCode\\\\\\\":\\\\\\\"删除应用成功\\\\\\\",\\\\\\\"message\\\\\\\":\\\\\\\"删除应用成功\\\\\\\",\\\\\\\"success\\\\\\\":true,\\\\\\\"traceId\\\\\\\":\\\\\\\"0bc0594d15954826692915817e****\\\\\\\"}\\\",\\\"errorCode\\\":\\\"删除应用成功\\\",\\\"message\\\":\\\"删除应用成功\\\",\\\"success\\\":true,\\\"traceId\\\":\\\"0ab2646915954826692568137d****\\\"}\" }"}
```

