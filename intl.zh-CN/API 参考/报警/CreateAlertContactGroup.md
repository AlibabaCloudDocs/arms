# CreateAlertContactGroup

调用CreateAlertContactGroup接口创建报警联系人分组。

************

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=CreateAlertContactGroup&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAlertContactGroup|系统规定参数，取值为`CreateAlertContactGroup`。 |
|ContactGroupName|String|是|TestGroup|报警联系人分组名称。 |
|ContactIds|String|是|12\* 23\* 34\*|要包含在报警联系人分组内的联系人ID。多个联系人ID以空格分隔。可调用SearchAlertContact接口来查询联系人ID，详情请参见[SearchAlertContact](~~130703~~)。 |
|RegionId|String|是|cn-hangzhou|地域ID。默认情况下请填写`cn-hangzhou`。 |
|ProxyUserId|String|否|1234123\*|内部参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ContactGroupId|String|446\*|报警联系人分组ID。 |
|RequestId|String|70675725-8F11-4817-8106-CFE0AD71\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateAlertContactGroup
&ContactGroupName=TestGroup
&ContactIds=12* 23* 34*
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateAlertContactGroupResponse>
	  <ContactGroupId>446*</ContactGroupId>
	  <RequestId>70675725-8F11-4817-8106-CFE0AD71****</RequestId>
</CreateAlertContactGroupResponse>
```

`JSON` 格式

```
{
    "ContactGroupId": "446*",
    "RequestId": "70675725-8F11-4817-8106-CFE0AD71****"
}
```

