# SearchEvents

调用SearchEvents接口查询报警事件记录。

报警事件记录，不是报警发送记录。是报警规则每分钟轮询判断后的事件记录。分为触发与未触发。触发的事件，如果没有在静默期中，将会被发送。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchEvents&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchEvents|系统规定参数，取值为`SearchEvents`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|AlertId|Long|否|123|报警规则ID，可调用SearchAlertRules接口获取（对应返回参数中的`Id`），更多信息，请参见[SearchAlertRules](~~175825~~)。 |
|Pid|String|否|atc889zkcf@d8deedfa9bf\*\*\*\*|报警关联应用的应用ID（PID）。 |
|CurrentPage|Integer|否|1|查询结果分页的页码。默认为`1`。 |
|PageSize|Integer|否|10|查询结果分页的每页项目数量。默认为`10`。 |
|AppType|String|否|TRACE|报警规则关联应用的类型：

 -   `TRACE`：应用监控。
-   `RETCODE`：前端监控。 |
|AlertType|Integer|否|4|报警规则类型：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus监控报警规则。 |
|IsTrigger|Integer|否|1|报警事件是否被触发，若不填写则查询全部。

 -   `1`：触发
-   `0`：未触发 |
|StartTime|Long|否|1595565300000|查询报警事件的开始时间的时间戳。格式为Unix Timestamp Long，单位为毫秒。默认为当前时间的前10分钟。 |
|EndTime|Long|否|1595568970000|查询报警事件的结束时间的时间戳。格式为Unix Timestamp Long，单位为毫秒。默认为当前时间。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IsTrigger|Integer|0|内部参数。 |
|PageBean|Struct| |返回结构体。 |
|Event|Array of Event| |报警事件列表。 |
|AlertId|Long|123|事件关联的报警规则ID。 |
|AlertName|String|alertName|事件关联的报警规则名称。 |
|AlertRule|String|\{\\"operator\\":\\"&\\",\\"rules\\":\[\{\\"aggregates\\":\\"AVG\\",\\"alias\\":\\"JVM\_线程总数\\",\\"measure\\":\\"appstat.jvm.ThreadCount\\",\\"nValue\\":1,\\"operator\\":\\"HOH\_DOWN\\",\\"value\\":50.0\}\]\}|事件关联的报警规则判断条件配置。 |
|AlertType|Integer|4|事件关联的报警规则类型（一般不展示）：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus监控报警规则。 |
|EventLevel|String|1|事件等级。 |
|EventTime|Long|1595569020000|事件发生时间的时间戳。 |
|Id|Long|123|事件记录ID。 |
|Links|List|\[ "http://arms.console.aliyun.com/apm?startTime=1595565300000&endTime=1595569246633&regionId=cn-hangzhou&pid=\*\*\*\*" \]|事件还原现场链接列表。 |
|Message|String|unknow紧急报警\\nip：172.27.XX.XX\\n应用名 = test\\nRegion = cn-shenzhen\\n异常信息 = \{\\"timestamp\\"：\\"1615447972235\\"\}|事件内容，为JSONString格式，键表示维度，值表示此维度的报警内容。 |
|PageNumber|Integer|1|查询结果分页的页码。 |
|PageSize|Integer|10|查询结果分页的每页项目数量。 |
|TotalCount|Integer|2|查询结果总数。 |
|RequestId|String|32940175-181B-4B93-966E-4BB69176\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchEvents
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchEventsResponse>
	  <PageBean>
 	       <TotalCount>2</TotalCount>
	        <PageSize>10</PageSize>
	        <PageNumber>1</PageNumber>
	        <Event>
	              <EventLevel>1</EventLevel>
	              <AlertType>4</AlertType>
 	             <AlertId>123</AlertId>
	              <AlertName>alertName</AlertName>
	              <Message>unknow紧急报警\nip：172.27.XX.XX\n应用名 = test\nRegion = cn-shenzhen\n异常信息 = {\"timestamp\"：\"1615447972235\"}</Message>
	              <EventTime>1595569020000</EventTime>
	              <Id>123</Id>
	              <AlertRule>{\"operator\":\"&amp;\",\"rules\":[{\"aggregates\":\"AVG\",\"alias\":\"JVM_线程总数\",\"measure\":\"appstat.jvm.ThreadCount\",\"nValue\":1,\"operator\":\"HOH_DOWN\",\"value\":50.0}]}</AlertRule>
	              <Links>[                     "http://arms.console.aliyun.com/apm?startTime=1595565300000&amp;endTime=1595569246633&amp;regionId=cn-hangzhou&amp;pid=****"                 ]</Links>
	        </Event>
	  </PageBean>
	  <RequestId>32940175-181B-4B93-966E-4BB69176****</RequestId>
	  <IsTrigger>0</IsTrigger>
</SearchEventsResponse>
```

`JSON`格式

```
{
    "PageBean": {
        "TotalCount": 2,
        "PageSize": 10,
        "PageNumber": 1,
        "Event": {
            "EventLevel": 1,
            "AlertType": 4,
            "AlertId": 123,
            "AlertName": "alertName",
            "Message": "unknow紧急报警\\nip：172.27.XX.XX\\n应用名 = test\\nRegion = cn-shenzhen\\n异常信息 = {\\\"timestamp\\\"：\\\"1615447972235\\\"}",
            "EventTime": 1595569020000,
            "Id": 123,
            "AlertRule": "{\\\"operator\\\":\\\"&amp;\\\",\\\"rules\\\":[{\\\"aggregates\\\":\\\"AVG\\\",\\\"alias\\\":\\\"JVM_线程总数\\\",\\\"measure\\\":\\\"appstat.jvm.ThreadCount\\\",\\\"nValue\\\":1,\\\"operator\\\":\\\"HOH_DOWN\\\",\\\"value\\\":50.0}]}",
            "Links": "[                     \"http://arms.console.aliyun.com/apm?startTime=1595565300000&amp;endTime=1595569246633&amp;regionId=cn-hangzhou&amp;pid=****\"                 ]"
        }
    },
    "RequestId": "32940175-181B-4B93-966E-4BB69176****",
    "IsTrigger": 0
}
```

