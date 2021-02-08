# ListServices

Queries all services in a region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=xtrace&api=ListServices&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListServices|The operation that you want to perform. Set the value to `ListServices`. |
|RegionId|String|Yes|cn-beijing|The region ID of the instance. For example, you can set the parameter to `cn-hangzhou` for the China \(Hangzhou\) region and `cn-beijing` for the China \(Beijing\) region. |
|AppType|String|No|XTRACE|The type of the service. The parameter is optional. You can set the parameter to `XTRACE`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1E2B6A4C-6B83-4062-8B6F-AEEC1FC47DED|The ID of the request. |
|Services|Array| |The information of the services. |
|Service| | | |
|Pid|String|123k456@abcc6efc437|The ID of the service. |
|RegionId|String|cn-hangzhou|The region ID of the instance. For example, the value `cn-hangzhou` indicates that the instance resides in the China \(Hangzhou\) region and `cn-beijing` indicates that the instance resides in the China \(Beijing\) region. |
|ServiceName|String|a3|The name of the service. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListServices
&RegionId=cn-beijing
&<Common request parameters>
```

Sample success responses

`XML` format

```
<Services>
      <Service>
            <ServiceName>a3</ServiceName>
            <Pid>aokcdqn3ly@741623b4e915df8</Pid>
            <RegionId>cn-hangzhou</RegionId>
      </Service>
</Services>
```

`JSON` format

```
{
  "Services": {
    "Service": [
      {
        "ServiceName": "a3",
        "Pid": "aokcdqn3ly@741623b4e915df8",
        "RegionId": "cn-hangzhou"
      }
      ]
    }
}
```

