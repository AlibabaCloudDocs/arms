# SearchAlertContactGroup

You can call this operation to query alert contact groups.

## Debugging

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=ARMS&api=SearchAlertContactGroup&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SearchAlertContactGroup|The operation that you want to perform. Set this value to `SearchAlertContactGroup`. |
|ContactGroupName|String|Yes|TestGroup|The name of the alert contact group that you want to query. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ContactGroups| | |Information about the alert contact groups that you queried. |
|ContactGroupId|Long|746|The ID of the alert contact group. |
|ContactGroupName|String|TestGroup|The name of the alert contact group. |
|CreateTime|Long|1529668855000|The time when the alert contact group was created. |
|UpdateTime|Long|1529668855000|The time when the alert contact group was updated. |
|UserId|String|xxxxxxxxxxx|The ID of the user. |
|RequestId|String|620BC657-3D59-4DC9-A5CE-D09CE3834C1D|The ID of the request. |

## Examples

Sample request

```

http://arms.cn-hangzhou.aliyun-inc.com:8099/alert/SearchAlertContactGroup.json?Region=hangzhou
&ContactGroupName=TestGroup

```

Sample success response

`XML` format

```
<SearchAlertContactGroup>
      <requestId>620BC657-3D59-4DC9-A5CE-D09CE3834C1D</requestId>
      <contactGroups>
              <contactGroup>
                     <contactGroupId>746</contactGroupId>
                     <contactGroupName>TestGroup1</contactGroupName>
                     <createTime>1529668855000</createTime>
                     <updateTime>1529668855000</updateTime>
                     <userId>xxxxxxxxxxx</userId>
              </contactGroup>
              <contactGroup>
                     <contactGroupId>3849</contactGroupId>
                     <contactGroupName>TestGroup2</contactGroupName>
                     <createTime>1561428915000</createTime>
                     <updateTime>1561428915000</updateTime>
                     <userId>xxxxxxxxxxx</userId>
              </contactGroup>
       </contactGroups>
</SearchAlertContactGroup>
```

`JSON` format

```
{
	"contactGroups":[
		{
			"createTime":1529668855000,
			"updateTime":1529668855000,
			"contactGroupName":"TestGroup1",
			"userId":"xxxxxxxxxxx",
			"contactGroupId":746
		},
		{
			"createTime":1561428915000,
			"updateTime":1561428915000,
			"contactGroupName":"TestGroup2",
			"userId":"xxxxxxxxxxx",
			"contactGroupId":3849
		}
	],
	"requestId":"620BC657-3D59-4DC9-A5CE-D09CE3834C1D"
}
```

## Error codes

The operation returns only common errors. For more information about errors that are common to all operations, see [API Error Center](https://error-center.alibabacloud.com/status/product/ARMS).

