# DeleteTraceApp

You can call this operation to delete an application with a specified ID and type.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.](https://api.aliyun.com/#product=ARMS&api=DeleteTraceApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteTraceApp|The parameter specified by the system. Valid values: `DeleteTraceApp` . |
|AppId|String|Yes|5406\*\*|The ID of the application to be deleted. You can call the SearchTraceAppByName operation to query the ID. For more information, see [SearchTraceAppByName](~~130676~~) . |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|Type|String|Yes|TRACE|The type of the application to be deleted. You can call the SearchTraceAppByName operation to query the type of the application. For more information, see [SearchTraceAppByName](~~130676~~) . The metric type. Valid values:

 -   `TRACE` : Application Monitoring
-   `RETCODE` : browser monitoring |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|\{"RequestId": "\#\#\#\*", "Data": "\{\\" code\\":200,\\" data\\":\\" \\\\\\ "code \\\\\\":200 ,\\\\\\ "data \\\\\\":true \\\\\\ "errorCode \\\\\\" :\\\\\\ "application deleted successfully \\\\\\" ,\\\\\\ "message \\\\\\" :\\\\\\ "application deleted successfully \\\\\\" ,\\\\\\ "success \\\\\\":true \\\\\\ "traceId \\\\\\" :\\" success \\\\\\ ":\\" traceId \\\\\\ ",\\code":\\"\\" Application deleted \\",\\" message\\":\\" application deleted \\",\\" success\\":true,\\" traceId\\":\\" 0 ab2646915954826256913687d \[\[\] \*\\"\}"\}|The response in JSON format, including the HTTP status code, error code, response message, and TraceId. |
|RequestId|String|46355DD8-FC56-40C5-BFC6-269DE4F9\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=DeleteTraceApp &AppId=5406 ** &RegionId=cn-hangzhou &Type=TRACE &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <DeleteTraceAppResponse> <RequestId> 46355DD8-FC56-40C5-BFC6-269DE4F9 **** </RequestId> <Data> {"code":200,"data":"{\" code\":200,\" The data\":true \" errorCode\"\" delete applications succeeded \",\" message\":\" Deleted application succeeded \",\" success\":true,\" traceId\":\" 0 bc0592d154826692915817e %*** \"}","errorCode":"deleted application success","message":"deleted application success","success":true,"traceId":"0 ab2646915954826692568137d"} </Data> * "</DeleteTraceAppResponse> 
   
```

`JSON`

```

     {"RequestId": "###*", "Data": "{\" code\":200,\" data\":\" \\\ "code \\\":200 ,\\\ "data \\\":true \\\ "errorCode \\\" :\\\ "application deleted successfully \\\" ,\\\ "message \\\" :\\\ "application deleted successfully \\\" ,\\\ "success \\\":true \\\ "traceId \\\" :\" success \\\ ":\" traceId \\\ ",\code":\"\" Application deleted \",\" message\":\" application deleted \",\" success\":true,\" traceId\":\" 0 ab2646915954826256913687d [[] *\"}"} 
   
```

