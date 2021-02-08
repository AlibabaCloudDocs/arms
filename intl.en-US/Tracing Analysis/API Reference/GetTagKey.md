# GetTagKey

Queries tag key in traced data.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=GetTagKey&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetTagKey|The operation that you want to perform. Set the value to `GetTagKey`. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|ServiceName|String|No|appTest|The name of the service. |
|SpanName|String|No|createOrder|The name of a span. |
|StartTime|Long|No|1575561600000|The beginning of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |
|EndTime|Long|No|1575622455686|The end of the time range to query. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |
|TagKeys|List|"TagKeys": \{ "TagKey": \[ "error.kind","span.kind"\]\}|The list of the tag keys. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetTagKey
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagKeys>
    <TagKey>date</TagKey>
    <TagKey>resultCount</TagKey>
    <TagKey>aTid</TagKey>
    <TagKey>dbName</TagKey>
    <TagKey>pid</TagKey>
    <TagKey>conf</TagKey>
    <TagKey>error</TagKey>
    <TagKey>type</TagKey>
    <TagKey>getSt</TagKey>
    <TagKey>eventSubmitDoGetConfig</TagKey>
    <TagKey>measures</TagKey>
    <TagKey>eventSubmitDoSelectTopoInfo</TagKey>
    <TagKey>span.kind</TagKey>
    <TagKey>eventSubmitDoGetDatas</TagKey>
    <TagKey>action</TagKey>
    <TagKey>startTime</TagKey>
    <TagKey>sn</TagKey>
    <TagKey>stageId</TagKey>
    <TagKey>st</TagKey>
    <TagKey>sampler.type</TagKey>
    <TagKey>k1</TagKey>
    <TagKey>IsCompleted</TagKey>
    <TagKey>sampler.param</TagKey>
    <TagKey>grpc.status</TagKey>
    <TagKey>param3</TagKey>
    <TagKey>userId</TagKey>
    <TagKey>param1</TagKey>
    <TagKey>param2</TagKey>
    <TagKey>reqId</TagKey>
    <TagKey>http.status_code</TagKey>
    <TagKey>component</TagKey>
    <TagKey>IntervalInSecond</TagKey>
    <TagKey>error.kind</TagKey>
    <TagKey>regionId</TagKey>
    <TagKey>metric</TagKey>
    <TagKey>lb</TagKey>
    <TagKey>eventSubmitDoGetRpcTypeInfoList</TagKey>
    <TagKey>_metric</TagKey>
    <TagKey>intervalMillis</TagKey>
    <TagKey>endTime</TagKey>
    <TagKey>bid</TagKey>
    <TagKey>did</TagKey>
    <TagKey>getEt</TagKey>
    <TagKey>db</TagKey>
    <TagKey>dimensions</TagKey>
</TagKeys>
<RequestId>7D6519C1-A92A-4F07-AC83-706D48204242</RequestId>
```

`JSON` format

```
{
    "TagKeys": {
        "TagKey": [
            "date",
            "resultCount",
            "aTid",
            "dbName",
            "pid",
            "conf",
            "error",
            "type",
            "getSt",
            "eventSubmitDoGetConfig",
            "measures",
            "eventSubmitDoSelectTopoInfo",
            "span.kind",
            "eventSubmitDoGetDatas",
            "action",
            "startTime",
            "sn",
            "stageId",
            "st",
            "sampler.type",
            "k1",
            "IsCompleted",
            "sampler.param",
            "grpc.status",
            "param3",
            "userId",
            "param1",
            "param2",
            "reqId",
            "http.status_code",
            "component",
            "IntervalInSecond",
            "error.kind",
            "regionId",
            "metric",
            "lb",
            "eventSubmitDoGetRpcTypeInfoList",
            "_metric",
            "intervalMillis",
            "endTime",
            "bid",
            "did",
            "getEt",
            "db",
            "dimensions"
        ]
    },
    "RequestId": "7D6519C1-A92A-4F07-AC83-706D48204242"
}
```

