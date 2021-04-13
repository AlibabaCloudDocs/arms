# DeleteScenario

Deletes a business monitoring job.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DeleteScenario&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteScenario|The operation that you want to perform. Set the value to DeleteScenario. |
|ScenarioId|Long|Yes|132|The ID of the business monitoring job. You can obtain the ID by calling the ListScenario operation. |
|RegionId|String|No|cn-zhangjaikou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|EA24D522-AD35-47B8-8CB2-ADBC382B\*\*\*\*|The ID of the request. |
|Result|Boolean|true|Indicates whether the request is successful.

 -   `true`: successful
-   `false`: failed |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DeleteScenario
&ScenarioId=132
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteScenarioResponse>
      <RequestId>EA24D522-AD35-47B8-8CB2-ADBC382B****</RequestId>
      <Result>true</Result>
</DeleteScenarioResponse>
```

`JSON` format

```
{
    "RequestId": "EA24D522-AD35-47B8-8CB2-ADBC382B****",
    "Result": true
}
```

