# QueryMetricByPage（应用监控）

调用QueryMetricByPage接口分页查询应用监控的相关监控指标。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=QueryMetricByPage&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryMetricByPage|系统规定参数，取值为`QueryMetricByPage`。 |
|EndTime|Long|是|1596183532000|结束时间的时间戳，精确到毫秒。 |
|IntervalInSec|Integer|是|60000|数据片的时间间隔，单位为毫秒，最小值为60000。 |
|Measures.N|RepeatList|是|pv|指标对应的测量数据，详情请参考[可查询的应用监控指标](/cn.zh-CN/API 参考/应用监控/QueryMetric（应用监控）.md)。最多可添加5个。|
|Metric|String|是|webstat.index|需要查询的指标，不可自定义输入，详情请参考[可查询的应用监控指标](/cn.zh-CN/API 参考/应用监控/QueryMetric（应用监控）.md)。|
|StartTime|Long|是|1595319532000|起始时间的时间戳，精确到毫秒。 |
|OrderBy|String|否|rpc|排序依据，可设为任一测量数据。 |
|Filters.N.Key|String|否|pid|筛选条件组合，必须添加`pid`和`regionId`条件，`pid`获取方式请参考[如何获取应用pid](#p_xyi_tr6_2w5)。|
|Filters.N.Value|String|否|xxx@74xxx|筛选条件组合，必须添加`pid`和`regionId`条件，`pid`获取方式请参考[如何获取应用pid](#p_xyi_tr6_2w5)。|
|Dimensions.N|RepeatList|否|\["detector\_browser","detector\_device"\]|指标对应的维度，详情请参考[可查询的应用监控指标](/cn.zh-CN/API 参考/应用监控/QueryMetric（应用监控）.md)。最多可添加5个。|
|Order|String|否|ASC|排序标准：

-   `ASC`：升序
-   `DESC`：降序 |
|RegionId|String|否|cn-hangzhou|地域ID。 |
|CurrentPage|Integer|否|1|查询结果的页码。非必填参数，如果不填写则默认为`1`。 |
|PageSize|Integer|否|10|查询结果的每页项目数量。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态，取值说明如下：

-   2XX：成功
-   3XX：重定向
-   4XX：请求错误
-   5XX：服务器错误 |
|Data|Struct| |返回结构体 |
|Items|List|\[\]|返回数据的数据结构体列表 |
|Page|Integer|1|查询结果的页码 |
|PageSize|Integer|10|查询结果的每页项目数量 |
|Total|Integer|0|查询结果的总项目数量 |
|Message|String|message|返回的信息 |
|RequestId|String|626037F5-FDEB-45B0-804C-B3C92797\*\*\*\*|请求ID |
|Success|Boolean|true|查询是否成功：

-   `true`：成功
-   `false`：失败 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=QueryMetricByPage
&EndTime=1596183532000
&IntervalInSec=60000
&Measures.1=pv
&Metric=webstat.index
&StartTime=1595319532000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<QueryMetricByPageResponse>
      <RequestId>626037F5-FDEB-45B0-804C-B3C92797****</RequestId>
      <Message>message</Message>
      <Data>
            <PageSize>10</PageSize>
            <Total>0</Total>
            <Page>1</Page>
            <Items>[]</Items>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</QueryMetricByPageResponse>
```

`JSON` 格式

```
{
    "RequestId": "626037F5-FDEB-45B0-804C-B3C92797****",
    "Message": "message",
    "Data": {
        "PageSize": 10,
        "Total": 0,
        "Page": 1,
        "Items": "[]"
    },
    "Code": 200,
    "Success": true
}
```

