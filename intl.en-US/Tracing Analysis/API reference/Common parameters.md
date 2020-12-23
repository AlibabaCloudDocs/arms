# Common parameters

This topic describes the request and response parameters that each API operation uses.

## Common request parameters

|Parameter|Type|Required?|Description|
|:--------|:---|:--------|:----------|
|Format|String|No|The format in which to return the response. Default value: JSON. Valid values: JSON and XML. |
|Version|String|Yes|The API version in a date format of YYYY-MM-DD. Set this value to 2019-08-08 |
|AccessKeyId|String|Yes|The AccessKey ID of your Alibaba Cloud account that is used to access SSL Certificates Service.|
|Signature|String|Yes|The signature string of the current request.|
|SignatureMethod|String|Yes|The algorithm used to create the request signature. Valid value: HMAC-SHA1 |
|Timestamp|String|Yes|The time at which the quest is signed. Specify the time in the ISO 8601 standard in the YYYY-MM-ddTHH:mm:ssZ format. The time must be in UTC. for example, 2013-01-10T12:00:00Z. |
|SignatureVersion|String|Yes|The signature version to use. Valid value: 1.0 |
|SignatureNonce|String|Yes|A unique and random number that is used to prevent replay attacks. Users must use different numbers for different requests. |
|ResourceOwnerAccount|String|No|The account that owns the resource to be accessed by the API request.|

Examples

```

      https://xtrace.cn-hangzhou.aliyuncs.com/?Action=GetTagKey &AccessKeyId=key-test &Format=JSON &RegionId=cn-hangzhou &SecureTransport=true &SignatureMethod=HMAC-SHA1 &SignatureVersion=1.0 &Timestamp=2020-03-18T06%3A06%3A30Z &Version=2019-08-08&hellip; 
    
```

## Common response parameters

API responses use the HTTP response format where a 2xx status code indicates a successful call and a 4xx or 5xx status code indicates a failed call. Responses can be returned in either the JSON or XML format. You can specify the response format in the request. The default response format is XML. Every response returns a unique RequestId regardless of whether the call is successful.

-   If a `2xx` HTTP status code is returned, the call is successful.
-   If a `4xx` or `5xx` HTTP status code returned, the call failed.

Sample success responses

-   XML format

    ```
    
            <? xml version="1.0" encoding="utf-8"? > <! -The root node of the Response. --> <operation name + Response> <! -Response tag --> <RequestId> response </RequestId> <! -The Returned result --> </API name + Response> 
          
    ```

-   JSON format

    ```
    
            {"RequestId":"4C467B38-3910-447 D-87BC-AC049166F216", /* the response data */ } 
          
    ```


