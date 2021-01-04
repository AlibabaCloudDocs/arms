# StartAlert

Starts an alert rule.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=StartAlert&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StartAlert|The operation that you want to perform. Set the value to `StartAlert`. |
|AlertId|String|Yes|1610\*\*\*|The ID of the alert rule. You can call the SearchAlertRules operation and view the `Id` parameter in the response. For more information, see [SearchAlertRules](~~175825~~). |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. Set the value to `cn-hangzhou`. |
|ProxyUserId|String|No|123412\*\*|The internal parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|IsSuccess|Boolean|true|Indicates whether the call was successful.

 -   `true`: The call was successful.
-   `false`: The call failed. |
|RequestId|String|27E653FA-5958-45BE-8AA9-14D884DC\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=StartAlert
&AlertId=1610***
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<StartAlertResponse>
	  <IsSuccess>true</IsSuccess>
	  <RequestId>27E653FA-5958-45BE-8AA9-14D884DC****</RequestId>
</StartAlertResponse>
```

`JSON` format

```
{
    "IsSuccess": true,
    "RequestId": "27E653FA-5958-45BE-8AA9-14D884DC****"
}
```

