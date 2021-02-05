# CreateAlertContactGroup

Creates an alert contact group.

************

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=CreateAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAlertContactGroup|The operation that you want to perform. Set the value to `CreateAlertContactGroup`. |
|ContactGroupName|String|Yes|TestGroup|The name of the alert contact group. |
|ContactIds|String|Yes|12\* 23\* 34\*|The IDs of contacts in the contact group. Separate multiple contact IDs with spaces. You can call the SearchAlertContact operation to query the contact IDs. For more information, see [SearchAlertContact](~~130703~~). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Default value: `cn-hangzhou`. |
|ProxyUserId|String|No|1234123\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactGroupId|String|446\*|The ID of the alert contact group. |
|RequestId|String|70675725-8F11-4817-8106-CFE0AD71\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=CreateAlertContactGroup
&ContactGroupName=TestGroup
&ContactIds=12* 23* 34*
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAlertContactGroupResponse>
	  <ContactGroupId>446*</ContactGroupId>
	  <RequestId>70675725-8F11-4817-8106-CFE0AD71****</RequestId>
</CreateAlertContactGroupResponse>
```

`JSON` format

```
{
    "ContactGroupId": "446*",
    "RequestId": "70675725-8F11-4817-8106-CFE0AD71****"
}
```

