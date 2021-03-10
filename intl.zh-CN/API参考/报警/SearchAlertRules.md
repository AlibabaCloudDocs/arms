# SearchAlertRules

调用SearchAlertRules接口查询报警规则。

************

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SearchAlertRules&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SearchAlertRules|系统规定参数，取值为`SearchAlertRules`。 |
|RegionId|String|是|cn-hangzhou|地域ID。 |
|Title|String|否|AlertRuleTitle|报警规则名称。 |
|Type|String|否|4|报警规则类型：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus监控报警规则。 |
|CurrentPage|Integer|否|1|查询结果分页的页码。默认为`1`。 |
|PageSize|Integer|否|20|查询结果分页的每页项目数量。默认为`10`。 |
|Pid|String|否|atc889zkcf@d8deedfa9bf\*\*\*\*|报警规则关联的ARMS应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr)。 |
|AppType|String|否|TRACE|报警规则对应的应用类型，分为以下类型：

 -   `TRACE`：应用监控报警规则
-   `RETCODE`：前端监控报警规则 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageBean|Struct| |返回结构体。 |
|AlertRules|Array of AlertRuleEntity| |报警规则列表。 |
|AlarmContext|Struct| |报警发送消息格式。 |
|AlarmContentSubTitle|String|TestSubTitle|报警内容子标题。 |
|AlarmContentTemplate|String|报警名称：$报警名称\\n筛选条件：$筛选\\n报警时间：$报警时间\\n报警内容：$报警内容\\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！|报警通知内容模板。 |
|Content|String|报警名称：$报警名称\\n筛选条件：$筛选\\n报警时间：$报警时间\\n报警内容：$报警内容\\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！|报警通知内容。 |
|SubTitle|String|test|报警通知子标题。 |
|AlertLevel|String|WARN|报警通知级别，目前只支持`WARN`。 |
|AlertRule|Struct| |报警规则判断条件列表。支持多个条件，条件间用“与逻辑”或“或逻辑”连接。 |
|Operator|String|\||报警规则判断逻辑。`&`表示“与”逻辑，`|`表示“或”逻辑。 |
|Rules|Array of Rule| |报警规则判断条件。 |
|Aggregates|String|AVG|报警判断规则的聚合逻辑：

 -   `AVG`：每分钟求平均
-   `SUM`：每分钟值求和
-   `MAX`：每分钟最大值
-   `MIN`：每分钟最小值 |
|Alias|String|调用响应时间\_ms|报警指标的展示文本。 |
|Measure|String|appstat.jvm.SystemDiskFree|报警规则数据指标，根据这些指标判断是否符合报警规则条件。更多信息，请参见[报警指标取值枚举](https://www.alibabacloud.com/help/zh/doc-detail/175825.htm?spm=a2c63.p38356.b99.373.61d25830rs3HHm#h2-url-4)。 |
|NValue|Integer|5|报警规则判断条件的数据请求范围，单位为分钟。例如，NValue=5表示每分钟报警将请求最近5分钟的数据。 |
|Operator|String|CURRENT\_GTE|报警规则判断条件的判断符号：

 -   CURRENT\_GTE：大于或等于
-   CURRENT\_LTE：小于或等于
-   PREVIOUS\_UP：环比上升百分比
-   PREVIOUS\_DOWN：环比下降百分比
-   HOH\_UP：与上小时同比上升百分比
-   HOH\_DOWN：与上小时同比下降百分比
-   DOD\_UP：与昨日同比上升百分比
-   DOD\_DOWN：与昨日同比下降百分比 |
|Value|Float|30|报警规则判断条件的判断阈值。 |
|AlertTitle|String|TestAlertRule|报警规则名称。 |
|AlertType|Integer|4|报警规则类型：

 -   `1`：基于下钻数据集的自定义监控报警规则。
-   `3`：基于平铺数据集的自定义监控报警规则。
-   `4`：前端监控报警规则，包含默认前端监控报警规则（AlertType=6）。
-   `5`：应用监控报警规则，包含默认应用监控报警规则（AlertType=7）。
-   `6`：默认前端监控报警规则。
-   `7`：默认应用监控报警规则。
-   `8`：链路追踪Tracing Analysis报警规则。
-   `101`：Prometheus监控报警规则。 |
|AlertVersion|Integer|1|报警规则版本，默认为`1`。 |
|AlertWay|List|null|报警通知发送方式：

 -   `SMS`：短信
-   `MAIL`：邮件
-   `DING_ROBOT`：钉钉机器人 |
|AlertWays|List|\["MAIL", "SMS", "DING\_ROBOT"\]|报警通知发送方式：

 -   `SMS`：短信
-   `MAIL`：邮件
-   `DING_ROBOT`：钉钉机器人 |
|Config|String|\{\\"continuous\\":true,\\"dataRevision\\":2\}|报警规则的配置项，格式为JSON字符串。

 **continuous**的值包括：

 -   `true`：每分钟均发送报警
-   `false`：打开报警静默期开关

 **dataRevision**表示未取得数据或者或数据为null值时的数据修订策略，包括：

 -   `0`：补零策略。
-   `1`：补一策略。
-   `2`：补null （默认补null），将不对数据做处理，无数据时将不会生成报警事件。 |
|ContactGroupIdList|String|381\*,572\*|报警规则中联系人分组ID，多个ID以半角逗号（,）分隔。 |
|ContactGroupIds|String|\[123, 234\]|报警联系人分组ID，格式为JSONArray。 |
|CreateTime|Long|1579508519683|报警规则创建时间的时间戳。 |
|Id|Long|123|报警规则ID。 |
|MetricParam|Struct| |报警规则关联应用信息配置。 |
|AppGroupId|String|DEFAULT|报警关联应用的应用子分组ID，适用于EDAS应用分组场景。 |
|AppId|String|123|ARMS应用的自增ID，可忽略。 |
|Dimensions|Array of Dimension| |报警规则判断条件中的维度条件。 |
|Key|String|rootIp|维度名称，包括以下值：

 -   `rpc`：接口名称
-   `rpcType`：接口调用类型（如HTTP、DUBBO）
-   `endpoint`：数据库名称
-   `rootIp`：机器IP地址 |
|Type|String|DISABLED|维度条件的类型，包含以下可选值：

 -   `STATIC`： 固定匹配此维度值需要填**dimensions.value**。
-   `ALL`：遍历所有维度值，按此接口所有接口名的指标依次判断，哪个接口触发阈值引起报警，就会在报警内容中体现该接口名，此时不需要填**dimensions.value**。
-   `DISABLE`：聚合所有维度值为一个值（求和），此时不需要填**dimensions.value**。 |
|Value|String|"127.0.0.1"|维度选项的值。 |
|Pid|String|9870ca99-8105-4da7-a3a4-d72dd1b1\*\*\*\*|报警规则关联的应用的ID。 |
|Type|String|DB|报警规则指标的类型。

 -   `txn`：应用监控入口调用量
-   `txn_type`：应用监控调用类型统计
-   `db`：数据库指标
-   `jvm`：JVM监控
-   `host`：主机监控
-   `exception`：异常接口调用 |
|Notice|Struct| |报警规则的生效时间范围和通知时间范围。 |
|EndTime|Long|1480607940000|报警规则生效时间范围的结束时间的时间戳，控制报警规则在每天24小时中的生效时间范围。格式为UNIX时间戳，其中年月日不生效，只有时分秒生效。 |
|NoticeEndTime|Long|1480607940000|报警规则通知时间范围的结束时间的时间戳，控制报警规则在每天24小时中的通知时间范围。格式为UNIX时间戳，其中年月日不生效，只有时分秒生效。 |
|NoticeStartTime|Long|1480521600000|报警规则通知时间范围的开始时间的时间戳，控制报警规则在每天24小时中的通知时间范围。格式为UNIX时间戳，其中年月日不生效，只有时分秒生效。 |
|StartTime|Long|1480521600000|报警规则生效时间范围的开始时间的时间戳，控制报警规则在每天24小时中的生效时间范围。格式为UNIX时间戳，其中年月日不生效，只有时分秒生效。 |
|RegionId|String|cn-hangzhou|报警规则所属的地域ID。 |
|Status|String|RUNNING|报警规则状态。`RUNNING`表示运行中，`STOPPED`表示已停止。 |
|TaskId|Long|123|基于任务的自定义监控报警规则所关联的ARMS任务ID。 |
|TaskStatus|String|""|内部字段。 |
|Title|String|AlertTest|报警名称。 |
|UpdateTime|Long|1480521600000|报警规则更新时间的时间戳。 |
|UserId|String|113197164949\*\*\*\*|报警规则所属用户的ID。 |
|PageNumber|Integer|1|查询结果分页页码。 |
|PageSize|Integer|20|查询结果分页的每页项目数量。 |
|TotalCount|Integer|23|查询结果总数。 |
|RequestId|String|34ED024E-9E31-434A-9E4E-D9D15C3\*\*\*\*|请求ID。 |

## 报警指标取值枚举

-   报警类型（metricParam.type）：TXN（应用监控入口调用量）
    -   此类报警维度（dimensions.key）：rpc（接口名称）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.txn.rt：入口调用响应时间（毫秒）
        -   appstat.txn.count：入口调用次数
        -   appstat.txn.errcount：入口调用错误次数
-   报警类型（metricParam.type）：TXN\_TYPE（应用监控调用类型统计）
    -   此类报警维度（dimensions.key）：rpcType（接口调用类型，如HTTP、DUBBO）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.inbound.rt：应用提供服务调用响应时间（毫秒）
        -   appstat.inbound.count：应用提供服务调用次数
        -   appstat.inbound.error：应用提供服务调用错误数
        -   appstat.outbound.rt：应用依赖服务调用响应时间（毫秒）
        -   appstat.outbound.count：应用依赖服务调用次数
        -   appstat.outbound.error：应用依赖服务调用错误数
-   报警类型（metricParam.type）：DB（数据库指标）
    -   此类报警维度（dimensions.key）：endpoint（数据库名称）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.database.rt：数据库调用响应时间（毫秒）
        -   appstat.database.count：数据库调用次数
        -   appstat.database.errcount：数据库调用错误次数
-   报警类型（metricParam.type）：JVM（JVM监控）
    -   此类报警维度（dimensions.key）：rootIp（机器IP地址）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.jvm.heap\_used：JVM堆内总内存量（字节）
        -   appstat.jvm.GcPsScavengeCount：JVM垃圾回收次数
        -   appstat.jvm.GcPsMarkSweepCount：JVM标记清除次数
        -   appstat.jvm.GcG1OldGenCount：JVM\_Old区G1GC次数
        -   appstat.jvm.GcG1YoungGenCount：JVM\_Young区G1GC次数
        -   appstat.jvm.gc.YoungGcCountInstant：JVM\_YoungGC次数
        -   appstat.jvm.gc.OldGcCountInstant：JVM\_FullGC次数
        -   appstat.jvm.gc.YoungGcTimeInstant：JVM\_YoungGC耗时（毫秒）
        -   appstat.jvm.gc.OldGcTimeInstant：JVM\_FullGC耗时（毫秒）
        -   appstat.jvm.ThreadCount：JVM\_线程总数
        -   appstat.jvm.non\_heap\_used：JVM非堆总使用内存量（字节）
        -   appstat.jvm.non\_heap\_max：JVM非堆内存最大值（字节）
        -   appstat.jvm.non\_heap\_init：JVM非堆内存初始值（字节）
        -   appstat.jvm.non\_heap\_committed：JVM非堆内存提交值（字节）
-   报警类型（metricParam.type）：HOST（主机监控）
    -   此类报警维度（dimensions.key）：rootIp（机器IP地址）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.jvm.SystemCpuUser：节点机用户使用CPU（百分比）
        -   appstat.jvm.SystemMemFree：节点机空闲内存（字节）
        -   appstat.jvm.SystemDiskFree：节点机空闲磁盘（字节）
        -   appstat.jvm.SystemNetInErrs：节点机接收错误报文数
        -   appstat.jvm.SystemNetOutErrs：节点机发送错误报文数
        -   appstat.jvm.SystemLoad：节点机系统负载
-   报警类型（metricParam.type）：EXCEPTION（异常接口调用）
    -   此类报警维度（dimensions.key）：rpc（接口名称）
    -   此类报警数据请求指标（alertRule.rules.measure）：
        -   appstat.exception.rt：应用异常接口调用响应时间（毫秒）
        -   appstat.exception.count：应用异常接口调用次数

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SearchAlertRules
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SearchAlertRulesResponse>
  <PageBean>
        <TotalCount>23</TotalCount>
        <PageSize>20</PageSize>
        <PageNumber>1</PageNumber>
        <AlertRules>
              <Status>RUNNING</Status>
              <TaskId>123</TaskId>
              <AlertVersion>1</AlertVersion>
              <ContactGroupIds>[123, 234]</ContactGroupIds>
              <Config>{\"continuous\":true,\"dataRevision\":2}</Config>
              <CreateTime>1579508519683</CreateTime>
              <Title>AlertTest</Title>
              <TaskStatus>""</TaskStatus>
              <AlertType>4</AlertType>
              <ContactGroupIdList>381*,572*</ContactGroupIdList>
              <UserId>113197164949****</UserId>
              <UpdateTime>1480521600000</UpdateTime>
              <AlertTitle>TestAlertRule</AlertTitle>
              <AlertLevel>WARN</AlertLevel>
              <RegionId>cn-hangzhou</RegionId>
              <Id>123</Id>
              <AlertWays>["MAIL", "SMS", "DING_ROBOT"]</AlertWays>
              <AlertWay>null</AlertWay>
              <AlarmContext>
                    <AlarmContentTemplate>报警名称：$报警名称\n筛选条件：$筛选\n报警时间：$报警时间\n报警内容：$报警内容\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！</AlarmContentTemplate>
                    <AlarmContentSubTitle>TestSubTitle</AlarmContentSubTitle>
                    <Content>报警名称：$报警名称\n筛选条件：$筛选\n报警时间：$报警时间\n报警内容：$报警内容\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！</Content>
                    <SubTitle>test</SubTitle>
              </AlarmContext>
              <AlertRule>
                    <Operator>|</Operator>
                    <Rules>
                          <Operator>CURRENT_GTE</Operator>
                          <NValue>5</NValue>
                          <Aggregates>AVG</Aggregates>
                          <Alias>调用响应时间_ms</Alias>
                          <Value>30</Value>
                          <Measure>appstat.jvm.SystemDiskFree</Measure>
                    </Rules>
              </AlertRule>
              <MetricParam>
                    <Type>DB</Type>
                    <AppId>123</AppId>
                    <AppGroupId>DEFAULT</AppGroupId>
                    <Pid>9870ca99-8105-4da7-a3a4-d72dd1b1****</Pid>
                    <Dimensions>
                          <Type>DISABLED</Type>
                          <Value>"127.0.0.1"</Value>
                          <Key>rootIp</Key>
                    </Dimensions>
              </MetricParam>
              <Notice>
                    <EndTime>1480607940000</EndTime>
                    <NoticeStartTime>1480521600000</NoticeStartTime>
                    <StartTime>1480521600000</StartTime>
                    <NoticeEndTime>1480607940000</NoticeEndTime>
              </Notice>
        </AlertRules>
  </PageBean>
  <RequestId>34ED024E-9E31-434A-9E4E-D9D15C3****</RequestId>
</SearchAlertRulesResponse>
```

`JSON`格式

```
{
    "PageBean": {
        "TotalCount": 23,
        "PageSize": 20,
        "PageNumber": 1,
        "AlertRules": {
            "Status": "RUNNING",
            "TaskId": 123,
            "AlertVersion": 1,
            "ContactGroupIds": "[123, 234]",
            "Config": "{\\\"continuous\\\":true,\\\"dataRevision\\\":2}",
            "CreateTime": 1579508519683,
            "Title": "AlertTest",
            "TaskStatus": "\"\"",
            "AlertType": 4,
            "ContactGroupIdList": "381*,572*",
            "UserId": "113197164949****",
            "UpdateTime": 1480521600000,
            "AlertTitle": "TestAlertRule",
            "AlertLevel": "WARN",
            "RegionId": "cn-hangzhou",
            "Id": 123,
            "AlertWays": "[\"MAIL\", \"SMS\", \"DING_ROBOT\"]",
            "AlertWay": "null",
            "AlarmContext": {
                "AlarmContentTemplate": "报警名称：$报警名称\\n筛选条件：$筛选\\n报警时间：$报警时间\\n报警内容：$报警内容\\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！",
                "AlarmContentSubTitle": "TestSubTitle",
                "Content": "报警名称：$报警名称\\n筛选条件：$筛选\\n报警时间：$报警时间\\n报警内容：$报警内容\\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！",
                "SubTitle": "test"
            },
            "AlertRule": {
                "Operator": "|",
                "Rules": {
                    "Operator": "CURRENT_GTE",
                    "NValue": 5,
                    "Aggregates": "AVG",
                    "Alias": "调用响应时间_ms",
                    "Value": 30,
                    "Measure": "appstat.jvm.SystemDiskFree"
                }
            },
            "MetricParam": {
                "Type": "DB",
                "AppId": 123,
                "AppGroupId": "DEFAULT",
                "Pid": "9870ca99-8105-4da7-a3a4-d72dd1b1****",
                "Dimensions": {
                    "Type": "DISABLED",
                    "Value": "\"127.0.0.1\"",
                    "Key": "rootIp"
                }
            },
            "Notice": {
                "EndTime": 1480607940000,
                "NoticeStartTime": 1480521600000,
                "StartTime": 1480521600000,
                "NoticeEndTime": 1480607940000
            }
        }
    },
    "RequestId": "34ED024E-9E31-434A-9E4E-D9D15C3****"
}
```

