# DeleteRetcodeApp

Deletes a browser monitoring task.

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
|Data|String|true|Indicates whether the task was deleted or failed to be deleted. |
|RequestId|String|01FF8DD9-A09C-47A1-895A-B6E321BE77B6|The ID of the request. |

## Examples

Sample requests

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/retcode/DeleteRetcodeApp.json?AppId=1231
&RegionId=cn-hangzhou

```

Sample success responses

`XML` format

```
<o>
       <data type="string">true</data>
       <requestId type="string">01FF8DD9-A09C-47A1-895A-B6E321BE77B6</requestId>
</o>
```

`JSON` format

```
{
	"requestId":"01FF8DD9-A09C-47A1-895A-B6E321BE77B6",
	"data":"true"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

