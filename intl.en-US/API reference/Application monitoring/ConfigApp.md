# ConfigApp

Turns on or off the main switch of an application monitoring agent, or queries the status of the main switch.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ConfigApp&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ConfigApp|The operation that you want to perform. Set the value to `ConfigApp`. |
|AppIds|String|Yes|abc@def,ghi@jkl|The ID of the application. Separate multiple IDs with commas \(,\). |
|Enable|String|Yes|true|Specifies whether to turns on or off the main switch of the agent. The monitoring stops after the switch is turned off. If you do not specify this parameter, the main switch status of the agent is queried.

 -   `true`: turns on the switch
-   `false`: turns off the switch |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|abc@def success\\nghi@jkl success\\n|The result of the operation or the main switch status of the agent. |
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ConfigApp
&AppIds=abc@def,ghi@jkl
&Enable=true
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ConfigAppResponse>
	  <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId>
	  <Data>abc@def success
	ghi@jkl success
	</Data>
</ConfigAppResponse>
```

`JSON` format

```
{
    "RequestId": "16AF921B-8187-489F-9913-43C808B4****",
    "Data": "abc@def success\nghi@jkl success\n"
}
```

