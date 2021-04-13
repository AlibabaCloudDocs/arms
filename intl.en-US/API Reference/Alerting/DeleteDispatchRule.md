# DeleteDispatchRule

Deletes the dispatch policy of a specified ID.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DeleteDispatchRule&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDispatchRule|The operation that you want to perform. Set the value to DeleteDispatchRule. |
|Id|String|Yes|12345|The ID of the dispatch policy. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|The ID of the request. |
|Success|Boolean|true|Indicates whether the request is successful.

-   `true`: successful
-   `false`: failed |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DeleteDispatchRule
&Id=12345
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteDispatchRuleResponse>
      <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId>
      <Success>true</Success>
</DeleteDispatchRuleResponse>
```

`JSON` format

```
{
    "RequestId": "16AF921B-8187-489F-9913-43C808B4****",
    "Success": true
}
```

