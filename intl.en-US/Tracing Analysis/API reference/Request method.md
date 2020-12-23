# Request method

To send a Tracing Analysis API request, you must send an HTTP GET request to the API endpoint of Tracing Analysis. You must include the operation-specific request parameters in the request. After you call the API, the system returns a response. The request and response are encoded in UTF-8.

## Request syntax

Tracing Analysis API operations use RPC protocol. You can call Tracing Analysis API operations by sending HTTP GET requests.

The request syntax is as follows:

```
http://Endpoint/?Action=xx&Parameters
```

where:

-   Endpoint: the endpoint of the Tracing Analysis API is xtrace.\[regionId\].aliyuncs.com.
-   Action: the operation that you want to perform. For example, to query the tag keys in the traced data, you must set the Action parameter to GetTagKey.
-   Version: the version of the API. Set the value to 2019-08-08.
-   Parameters: the request parameters for the operation. Separate multiple parameters with ampersands \(&\).

    Request parameters include both common parameters and operation-specific parameters. Common request parameters include the API version and authentication-related parameters. For more information, see [Common parameters](/intl.en-US/API reference/Common parameters.md).


The following example demonstrates how to call the GetTagKey operation to query the tag keys in the traced data:

**Note:** The examples in this document are formatted to improve readability.

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

