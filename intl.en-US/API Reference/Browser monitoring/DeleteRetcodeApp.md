# DeleteRetcodeApp

Deletes a frontend monitoring task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DeleteRetcodeApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteRetcodeApp|The operation that you want to perform. Set the value to `DeleteRetcodeApp`. |
|AppId|String|Yes|1231|The ID of the application. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|true|Indicates whether the frontend monitoring task is deleted or fails to be deleted. Valid values:

 -   `true`: The task is deleted.
-   `false`: The task fails to be deleted. |
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DeleteRetcodeApp
&AppId=1231
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteRetcodeAppResponse>
       <data>true</data>
       <requestId>01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
</DeleteRetcodeAppResponse>
```

`JSON` format

```
{
    "requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
    "data":"true"
}
```

