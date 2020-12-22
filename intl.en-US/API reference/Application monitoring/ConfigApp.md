# ConfigApp

You can call this operation to enable or disable the master switch of an application monitoring Agent, or query the status of the master switch of an Agent.

****

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ConfigApp|The parameter specified by the system. Valid values: `ConfigApp` . |
|AppIds|String|Yes|abc@def,ghi@jkl|The ID of the application. Multiple PID are separated by commas \(,\). |
|Enable|String|Yes|true|Specifies whether to enable or disable the Agent function of one or more applications. The monitoring stops after the switch is turned off. If this parameter is not specified, the Agent statuses of the target application are queried.

-   `true` : enable EDAs Agent .
-   `false` : Agent is disabled . |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|abc@def success\\nghi@jkl success\\n|Whether the operation is successful or the Agent status of the target application |
|RequestId|String|16AF921B-8187-489F-9913-43C808B4\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```

     http(s)://[Endpoint]/? Action=ConfigApp &AppIds=abc @ def,ghi @ jkl &Enable=true &RegionId=cn-hangzhou &<common request parameters> 
   
```

Sample success responses

`XML` format

```

     <ConfigAppResponse> <RequestId>16AF921B-8187-489F-9913-43C808B4****</RequestId> <Data>abc@def success ghi@jkl success </Data> </ConfigAppResponse> 
   
```

`JSON`

```

     { "RequestId": "16AF921B-8187-489F-9913-43C808B4****", "Data": "abc@def success\nghi@jkl success\n" } 
   
```

