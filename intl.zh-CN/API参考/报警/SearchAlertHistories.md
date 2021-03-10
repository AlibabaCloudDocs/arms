# SearchAlertHistories

调用SearchAlertHistories接口查询报警规则的报警发送记录。

********

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertHistories&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertHistories|系统规定参数，取值为`SearchAlertHistories`。 |
|RegionId|String|是|cn-hangzhou|地域ID。默认为`cn-hangzhou`。 |
|AlertId|Long|否|123|报警规则ID，可调用SearchAlertRules接口获取（对应返回参数中的`Id`），详情请参见[SearchAlertRules](~~175825~~)。 |
|AlertType|Integer|否|4|报警规则类型：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus报警规则。 |
|CurrentPage|Integer|否|1|查询结果分页的页码。默认为`1`。 |
|PageSize|Integer|否|10|查询结果分页的每页项目数量。默认为`10`。 |
|StartTime|Long|否|1595568910000|查询报警历史记录的开始时间的时间戳。格式为Unix Timestamp Long，单位为毫秒。默认为当前时间的前10分钟。 |
|EndTime|Long|否|1579499626000|查询报警历史记录的结束时间的时间戳。格式为Unix Timestamp Long，单位为毫秒。默认为当前时间。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回结构体 |
|AlarmHistories|Array of AlarmHistory| |报警历史对象列表 |
|AlarmContent|String|"报警名称：Alert1\\n报警时间：2020-07-24 12:14:00\\n报警内容：共有4条记录触发异常：\*\*\*\*"|报警内容 |
|AlarmResponseCode|Integer|200|报警投递返回的状态码 |
|AlarmSources|String|https://oapi.dingtalk.com/robot/send?access\_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca\*\*\*\*|报警Webhook（如钉钉机器人Webhook地址） |
|AlarmTime|Long|1595564179000|报警发送时间 |
|AlarmType|Integer|4|报警规则类型（默认为4）：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus监控报警规则。 |
|Emails|String|someone@example.com|接收报警的邮箱地址 |
|Id|Long|123|报警发送记录ID |
|Phones|String|1381111\*\*\*\*|接收报警的手机号码 |
|StrategyId|String|""|内部字段 |
|Target|String|""|内部字段 |
|UserId|String|113197164949\*\*\*\*|用户ID |
|PageNumber|Integer|1|查询结果分页的页码 |
|PageSize|Integer|10|查询结果分页的每页项目数量 |
|TotalCount|Integer|2|查询结果总数 |
|RequestId|String|2FC13182-B9AF-4E6B-BE51-72669B7C\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchAlertHistories
&RegionId=cn-hangzhou
&AlertId=123
&StartTime=1579499026000
&EndTime=1579499626000
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchAlertHistoriesResponse>
  <PageBean>
        <TotalCount>2</TotalCount>
        <PageSize>10</PageSize>
        <PageNumber>1</PageNumber>
        <AlarmHistories>
              <Target>""</Target>
              <Phones>1381111****</Phones>
              <AlarmTime>1595564179000</AlarmTime>
              <UserId>113197164949****</UserId>
              <AlarmResponseCode>200</AlarmResponseCode>
              <AlarmType>4</AlarmType>
              <StrategyId>""</StrategyId>
              <AlarmContent>"报警名称：Alert1\n报警时间：2020-07-24 12:14:00\n报警内容：共有4条记录触发异常：****"</AlarmContent>
              <Emails>someone@example.com</Emails>
              <Id>123</Id>
              <AlarmSources>https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****</AlarmSources>
        </AlarmHistories>
  </PageBean>
  <RequestId>2FC13182-B9AF-4E6B-BE51-72669B7C****</RequestId>
</SearchAlertHistoriesResponse>
```

`JSON`格式

```
{
    "PageBean": {
        "TotalCount": 2,
        "PageSize": 10,
        "PageNumber": 1,
        "AlarmHistories": {
            "Target": "\"\"",
            "Phones": "1381111****",
            "AlarmTime": 1595564179000,
            "UserId": "113197164949****",
            "AlarmResponseCode": 200,
            "AlarmType": 4,
            "StrategyId": "\"\"",
            "AlarmContent": "\"报警名称：Alert1\\n报警时间：2020-07-24 12:14:00\\n报警内容：共有4条记录触发异常：****\"",
            "Emails": "someone@example.com",
            "Id": 123,
            "AlarmSources": "https://oapi.dingtalk.com/robot/send?access_token=91f2f65002fefe0ab9b71e6590c5ca504348cad742ff01e9c8ab204439ca****"
        }
    },
    "RequestId": "2FC13182-B9AF-4E6B-BE51-72669B7C****"
}
```

