# ApplyScenario

Creates or updates a business monitoring job.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ApplyScenario&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ApplyScenario|The operation that you want to perform. Set the value to ApplyScenario. |
|AppId|String|Yes|b590lhguqs@28f515462f\*\*\*\*\*\*|The ID of the application. |
|Config|Json|Yes|\{"rpcType":"0","nameMatchType":"EQUALS","service":"/api/pop/test","operator":"and","filterItems":\[\{"type":"HttpHeaders","key":"uid","opt":"==","value":"123456789"\}\],"group":\{"type":"HttpRequestParameters","key":"name"\}\}|The configuration of the business monitoring job. The value is a JSON string. For more information about this parameter, see the following additional information about the **Config** parameter. |
|Name|String|Yes|Test POP business monitoring|The name of the business monitoring job. |
|UpdateOption|Boolean|Yes|false|Specifies whether the operation is an update operation.

 -   `true`: update
-   `false`: insert |
|RegionId|String|No|cn-zhangjaikou|The ID of the region. |
|Scenario|String|No|USER-DEFINED|The scenario where you want to use the business monitoring job. Valid values:

 -   `USER-DEFINED`: user-defined. This is the default value.
-   `EDAS-ROLLOUT`: application release in Enterprise Distributed Application Service \(EDAS\)
-   `OAM-ROLLOUT`: application release based on Open Application Model \(OAM\)
-   `MSC-CANARY`: canary release based on Microservice Engine \(MSE\) |
|Sign|String|No|a9f8\*\*\*\*|The code of the business monitoring job. This parameter is not required when you create a business monitoring job. However, this parameter is required when you update a business monitoring job. |
|SnTransfer|Boolean|No|false|Specifies whether the coloring sign is transparently passed down to downstream application nodes in the trace.

 -   `true`
-   `false`: This is the default value. |
|SnStat|Boolean|No|false|Specifies whether to count traffic based on the coloring sign.

 -   `true`
-   `false`: This is the default value. |
|SnDump|Boolean|No|false|Specifies whether to record business parameters to the trace marked with the coloring sign.

 -   `true`
-   `false`: This is the default value. |
|SnForce|Boolean|No|false|Specifies whether traffic in the trace marked with the coloring sign is all collected.

 -   `true`
-   `false`: This is the default value. |

## Additional information about the **Config** parameter

**JSON string example and description**

```

{
    "rpcType":"0",   //The service type. 0: HTTP ingress. 255: Kubernete Pod Metadata.
    "nameMatchType":"EQUALS",   //The matching mode of the service name. EQUALS: equal. STARTSWITH: equal to the start. CONTAINS: contains. ENDSWITH: equal to the end. PATTERNS: mode matching.
    "service":"/api/pop/test",   // The name of the service.
    "operator":"and",   //The relationship among filter rules. and: All the rules are met. or: A rule is met.
    "filterItems": //The filter rules.
        [{
            "type":"HttpHeaders",   //The matching parameters for the filter rules. For more information, see the next section.
            "key":"uid",   //The value of the key that matches the filter field.
            "opt":"==",   //The matching mode. Support ==, !=, and contains.
            "value":"123456789"   //The threshold of the filter field.
        }],
    "group":   //The grouping rule.
        {
            "type":"HttpRequestParameters",   //The matching parameters for the grouping rule. For more information, see the next section.
            "key":"name"   //The value of the key that matches the grouping rule.
        }
}

```

**Matching parameters for the filter rules**

When rpcType is set to 0, the service type is HTTP ingress and the matching parameters are the following parameters:

-   HttpRequestParameters
-   HttpHeaders
-   HttpCookies
-   HttpMethod
-   HttpPathVariables

When rpcType is set to 255, the service type is Kubernete Pod Metadata and the matching parameters are the following parameters:

-   k8sPodLabel
-   k8sPodAnnotation
-   k8sPodName
-   k8sPodNamespace
-   k8sPodUID
-   k8sPodIp
-   k8sPodServiceAccount

**Matching parameters for the grouping rule**

When rpcType is set to 0, the service type is HTTP ingress and the matching parameters are the following parameters:

-   HttpRequestParameters
-   HttpHeaders
-   HttpCookies
-   HttpMethod
-   HttpPathVariables

When rpcType is set to 255, the service type is Kubernete Pod Metadata and the matching parameters are the following parameters:

-   k8sPodLabel
-   k8sPodAnnotation
-   k8sPodName
-   k8sPodNamespace
-   k8sPodUID
-   k8sPodIp
-   k8sPodServiceAccount

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|EA24D522-AD35-47B8-8CB2-ADBC38\*\*\*\*\*\*|The ID of the request. |
|Result|String|2b97\*\*\*\*|The code of the business monitoring job, which is the coloring sign. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ApplyScenario
&AppId=b590lhguqs@28f515462f******
&Config=
{
    "rpcType":"0",
    "nameMatchType":"EQUALS",
    "service":"/api/pop/test",
    "operator":"and",
    "filterItems":
        [{
            "type":"HttpHeaders",
            "key":"uid",
            "opt":"==",
            "value":"123456789"
        }],
    "group":
        {
            "type":"HttpRequestParameters",
            "key":"name"
        }
}
&Name=Test POP business monitoring
&Sign=a9f8****
&UpdateOption=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ApplyScenarioResponse>
      <RequestId>EA24D522-AD35-47B8-8CB2-ADBC38******</RequestId>
      <Result>2b97****</Result>
</ApplyScenarioResponse>
```

`JSON` format

```
{
    "RequestId": "EA24D522-AD35-47B8-8CB2-ADBC38******",
    "Result": "2b97****"
}
```

