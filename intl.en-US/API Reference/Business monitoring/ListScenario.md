# ListScenario

Queries detailed information of a business monitoring job.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=ListScenario&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListScenario|The operation that you want to perform. Set the value to ListScenario. |
|AppId|String|Yes|b590lhguqs@28f515462\*\*\*\*\*\*|The ID of the application. |
|Name|String|Yes|Test business monitoring|The name of the business monitoring job. |
|RegionId|String|No|cn-zhangjaikou|The ID of the region. |
|Scenario|String|No|USER-DEFINED|The scenario where the business monitoring job is used. Valid values:

 -   `USER-DEFINED`: user-defined. This is the default value.
-   `EDAS-ROLLOUT`: application release in Enterprise Distributed Application Service \(EDAS\)
-   `OAM-ROLLOUT`: application release based on Open Application Model \(OAM\)
-   `MSC-CANARY`: canary release based on Microservice Engine \(MSE\) |
|Sign|String|No|a9f8\*\*\*\*|The code of the business monitoring job. Set this parameter when you know the code of the business monitoring job you want to query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ArmsScenarios|Array of ArmsScenarios| |The detailed information of the business monitoring job. |
|AppId|String|b590lhguqs@28f515462\*\*\*\*\*\*|The ID of the application. |
|CreateTime|String|1585214916000|The time when the business monitoring job was created. |
|Extensions|String|\{"\_MODE": "CUSTOM-TRANSACTION","\_SCENARIO": "USER-DEFINED"\}|The extended information. The value is a JSON string. |
|Id|Long|132|The ID of the business monitoring job. |
|Name|String|Test business monitoring|The name of the business monitoring job. |
|RegionId|String|cn-zhangjiakou|The ID of the region. |
|Sign|String|a9f8\*\*\*\*|The code of the business monitoring job. |
|UpdateTime|String|1585214916000|The time when the business monitoring job was updated. |
|UserId|String|113197164949\*\*\*\*|The ID of the user. |
|RequestId|String|98027D1F-3AEB-492C-A4AA-E9217992\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListScenario
&AppId=b590lhguqs@28f515462******
&Name=Test business monitoring
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListScenarioResponse>
  <RequestId>98027D1F-3AEB-492C-A4AA-E9217992****</RequestId>
  <ArmsScenarios>
        <AppId>b590lhguqs@28f515462******</AppId>
        <UserId>113197164949****</UserId>
        <CreateTime>1585214916000</CreateTime>
        <UpdateTime>1585214916000</UpdateTime>
        <Sign>a9f8****</Sign>
        <RegionId>cn-zhangjiakou</RegionId>
        <Id>132</Id>
        <Extensions>{"_MODE": "CUSTOM-TRANSACTION","_SCENARIO": "USER-DEFINED"}</Extensions>
        <Name>Test business monitoring </Name>
  </ArmsScenarios>
</ListScenarioResponse>
```

`JSON` format

```
{
    "RequestId": "98027D1F-3AEB-492C-A4AA-E9217992****",
    "ArmsScenarios": {
        "AppId": "b590lhguqs@28f515462******",
        "UserId": "113197164949****",
        "CreateTime": 1585214916000,
        "UpdateTime": 1585214916000,
        "Sign": "a9f8****",
        "RegionId": "cn-zhangjiakou",
        "Id": 132,
        "Extensions": "{\"_MODE\": \"CUSTOM-TRANSACTION\",\"_SCENARIO\": \"USER-DEFINED\"}",
        "Name": "Test business monitoring"
    }
}
```

