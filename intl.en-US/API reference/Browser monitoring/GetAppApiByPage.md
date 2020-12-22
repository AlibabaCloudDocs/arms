# GetAppApiByPage

Queries the interfaces of browser monitoring by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetAppApiByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAppApiByPage|The operation that you want to perform. Set the value to `GetAppApiByPage`. |
|CurrentPage|Integer|Yes|1|The number of the page to return. |
|EndTime|Long|Yes|1600066800000|The end of the time range to query. Unit: milliseconds. |
|PId|String|Yes|xxx@74xxx|The unique identifier of the application. For information about how to obtain the `pid`, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186822.htm?spm=a2c63.p38356.b99.166.5a83372fBJ2uK9#title-ref-s31-44g). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|StartTime|Long|Yes|1600063200000|The beginning of the time range to query. Unit: milliseconds. |
|PageSize|Integer|No|10|The number of entries to return on each page. |
|IntervalMills|Integer|No|60000|The time interval between the data shards to be queried. Unit: milliseconds. Minimum value: 60,000. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|Integer|200|The status of the API. Valid values:

 -   2XX: success
-   3XX: retried
-   4XX: request error
-   5XX: server error |
|Data|Struct| |The returned data struct. |
|Items|List|\[\]|The information of the API. |
|Page|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|Total|String|0|The sum of queries. |
|Message|String|message|The returned message. |
|RequestId|String|B6A00968-82A8-4F14-9D1B-B53827DB\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the query was successful. Valid values:

 -   `true`: The call was successful.
-   `false`: The call failed. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetAppApiByPage
&CurrentPage=1
&EndTime=1600066800000
&PId=xxx@74xxx
&RegionId=cn-hangzhou
&StartTime=1600063200000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetAppApiByPageResponse>
	  <RequestId>B6A00968-82A8-4F14-9D1B-B53827DB****</RequestId>
	  <Message>message</Message>
	  <Data>
		    <PageSize>10</PageSize>
		    <Total>0</Total>
		    <Page>1</Page>
		    <Items>[]</Items>
	  </Data>
	  <Code>200</Code>
	  <Success>true</Success>
</GetAppApiByPageResponse>
```

`JSON` format

```
{
    "RequestId": "B6A00968-82A8-4F14-9D1B-B53827DB****",
    "Message": "message",
    "Data": {
        "PageSize": 10,
        "Total": 0,
        "Page": 1,
        "Items": "[]"
    },
    "Code": 200,
    "Success": true
}
```

