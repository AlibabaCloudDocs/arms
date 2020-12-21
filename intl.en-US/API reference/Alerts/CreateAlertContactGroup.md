# CreateAlertContactGroup

You can call this operation to create an alert contact group.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=CreateAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAlertContactGroup|The operation that you want to perform. Set this value to `CreateAlertContactGroup`. |
|ContactGroupName|String|Yes|TestGroup|The name of the alert contact group that you want to create. |
|ContactIds|String|Yes|1234212343|The alert contact ID. If multiple contact IDs are available, separate them with spaces. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactGroupId|String|4466|The ID of the alert contact group that you created. |
|RequestId|String|E9354A61-9535-4CB3-8E1B-C12E177D2450|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/CreateAlertContactGroup.json?ContactGroupName=TestGroup
&ContactIds=1234212343
&RegionId=cn-hangzhou

```

Sample success response

`XML` format

```
<CreateAlertContactGroup>
      <RequestId>E9354A61-9535-4CB3-8E1B-C12E177D2450</RequestId>
      <ContactGroupId>4466</ContactGroupId>
</CreateAlertContactGroup>
```

`JSON` format

```
{
	"requestId":"E9354A61-9535-4CB3-8E1B-C12E177D2450",
	"contactGroupId":"4466"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

