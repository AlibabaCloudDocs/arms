# DescribeTraceLicenseKey

Queries the license key for application monitoring.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=DescribeTraceLicenseKey&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeTraceLicenseKey|The operation that you want to perform. Set the value to `DescribeTraceLicenseKey`. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LicenseKey|String|b590lhguqs@3a75d95f218\*\*\*\*|The license key for application monitoring. |
|RequestId|String|29053944-6FE5-4240-8927-10095ECE\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DescribeTraceLicenseKey
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeTraceLicenseKeyResponse>
	  <RequestId>29053944-6FE5-4240-8927-10095ECE****</RequestId>
	  <LicenseKey>b590lhguqs@3a75d95f2183b9b</LicenseKey>
</DescribeTraceLicenseKeyResponse>
```

`JSON` format

```
{
	"RequestId": "29053944-6FE5-4240-8927-10095ECE****",
	"LicenseKey": "b590lhguqs@3a75d95f2183b9b"
}
```

