# Common parameters

This topic describes the request and response parameters that each API operation uses.

## Common request parameters

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|The format in which to return the response. Valid values: JSON and XML. Default value: JSON. |
|Version|String|Yes|The version number of the API. The value is in the YYYY-MM-DD format. Set this value to 2019-08-08 |
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Yes|The signature string of the current request.|
|SignatureMethod|String|Yes|The encryption method of the signature string. Set the value to HMAC-SHA1 |
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the YYYY-MM-ddTHH:mm:ssZ format. The time must be in UTC. Example: 2013-01-10T12:00:00Z, which specifies 20:00:00 on January 10, 2013 \(UTC+8\). |
|SignatureVersion|String|Yes|The version of the signature encryption algorithm. Set the value to 1.0 |
|SignatureNonce|String|Yes|A unique and random number that is used to prevent replay attacks. You must use different numbers for multiple requests. |
|ResourceOwnerAccount|String|No|The account that owns the resource to be accessed by the API request.|

Sample requests

```
https://xtrace.cn-hangzhou.aliyuncs.com/?Action=GetTagKey
&AccessKeyId=key-test
&Format=JSON
&RegionId=cn-hangzhou
&SecureTransport=true
&SignatureMethod=HMAC-SHA1
&SignatureVersion=1.0
&Timestamp=2020-03-18T06%3A06%3A30Z
&Version=2019-08-08
…
```

## Common response parameters

Responses can be returned in either the JSON or XML format. You can specify the response format in the request. The default response format is XML. Every response returns a unique RequestId regardless of whether the call is successful.

-   A `2xx` HTTP status code indicates a successful call.
-   A `4xx` or `5xx` HTTP status code indicates a failed call.

Sample success responses

-   XML format

    ```
    <? xml version="1.0" encoding="utf-8"? > 
        <!--Root node of the response-->
        <Operation name+Response>
            <!--Return request tag-->
            <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!--Return result data-->
        </Operation name+Response>
                            
    ```

-   JSON format

    ```
    {
        "RequestId":"4C467B38-3910-447D-87BC-AC049166F216",
        /*Returned data*/
        }
    ```


