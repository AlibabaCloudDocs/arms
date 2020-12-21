# ImportAppAlertRules

You can call this operation to import application alert rules.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=ImportAppAlertRules&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ImportAppAlertRules|The operation that you want to perform. Set this value to `ImportAppAlertRules`. |
|ContactGroupIds|String|Yes|1234|The ID of the alert contact group. |
|Pids|String|Yes|xxxxxxxxx|The PIDs. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |
|TemplateAlertId|String|Yes|324324234|The ID of the alert template. |
|IsAutoStart|Boolean|No|true|Specifies whether the rule automatically starts to apply. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|399363 399364|The data returned. |
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C647A|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/ImportAppAlertRules.json?ContactGroupIds=1234
&Pids=xxxxxxxxx
&RegionId=cn-hangzhou
&TemplateAlertId=324324234

```

Sample success response

`XML` format

```
<ImportAppAlertRules>
       <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C647A</RequestId>
       <Data>399363 399364</Data>
</ImportAppAlertRules>
```

`JSON` format

```
{
	"requestId":"A5EC8221-08F2-4C95-9AF1-49FD998C647A",
	"data":"399363 399364"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

