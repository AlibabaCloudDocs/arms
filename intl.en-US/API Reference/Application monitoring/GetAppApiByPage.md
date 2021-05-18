# GetAppApiByPage

Queries the APIs of frontend monitoring by page.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=GetAppApiByPage&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetAppApiByPage|The operation that you want to perform. Set the value to `GetAppApiByPage`. |
|CurrentPage|Integer|Yes|1|The number of the page to return. |
|EndTime|Long|Yes|1600066800000|The end of the time range to query. Unit: milliseconds. |
|PId|String|Yes|xxx@74xxx|The process identifier \(PID\) of the application. For information about how to obtain the `PID`, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/183682.htm?spm=a2c63.l28256.b99.342.252412727XCKUD#h2-url-3). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|StartTime|Long|Yes|1600063200000|The beginning of the time range to query. Unit: milliseconds. |
|PageSize|Integer|No|10|The number of entries to return on each page. |
|IntervalMills|Integer|No|60000|The time interval between the data shards to be queried. Unit: milliseconds. Minimum value: 60000. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Code|Integer|200|The HTTP status code returned for the request. Valid values:

 -   2XX: The request is successful.
-   3XX: A redirection message is returned.
-   4XX: The request is invalid.
-   5XX: A server error occurs. |
|Data|Struct| |The struct returned. |
|Items|List|\[\]|The information about the API. |
|Page|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|Total|String|0|The total number of returned entries. |
|Message|String|message|The message returned. |
|RequestId|String|B6A00968-82A8-4F14-9D1B-B53827DB\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the call is successful. Valid values:

 -   `true`: The call is successful.
-   `false`: The call fails. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetAppApiByPage
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

