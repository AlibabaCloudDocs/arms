# DescribeTraceLicenseKey

调用DescribeTraceLicenseKey接口列出LicenseKey。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=DescribeTraceLicenseKey&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeTraceLicenseKey|系统规定参数，取值为`DescribeTraceLicenseKey`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|LicenseKey|String|b590lhguqs@3a75d95f218\*\*\*\*|应用的LicenseKey。 |
|RequestId|String|29053944-6FE5-4240-8927-10095ECE\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeTraceLicenseKey
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeTraceLicenseKeyResponse>
	  <RequestId>29053944-6FE5-4240-8927-10095ECE****</RequestId>
	  <LicenseKey>b590lhguqs@3a75d95f2183b9b</LicenseKey>
</DescribeTraceLicenseKeyResponse>
```

`JSON`格式

```
{
	"RequestId": "29053944-6FE5-4240-8927-10095ECE****",
	"LicenseKey": "b590lhguqs@3a75d95f2183b9b"
}
```

