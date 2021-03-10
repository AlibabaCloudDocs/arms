# ImportAppAlertRules

调用ImportAppAlertRules接口创建应用报警规则。

**说明：** **ImportAppAlertRules**接口仅适合于导入应用监控和前端监控报警规则，包括系统自动生成的应用监控和前端监控报警规则。该接口不适用于导入自定义监控报警规则、Prometheus监控报警规则、默认紧急报警规则等。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=ImportAppAlertRules&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ImportAppAlertRules|系统规定参数，取值为`ImportAppAlertRules`。 |
|Pids|String|是|\["atc889zkcf@d8deedfa9bfxxxx", "acd129bfcf@d5daebfa6cdxxxx"\]|常见报警规则关联的ARMS应用ID（即PID），格式为JsonArrayListStr。 |
|RegionId|String|是|cn-hangzhou|应用报警规则关联的应用所属地域的ID。 |
|TemplateAlertId|String|否|324324234|报警模板ID。**TemplateAlertId**和**TemplageAlertConfig**必须至少填写一个。如果两个参数都填写，则**TemplateAlertId**优先。 |
|ContactGroupIds|String|否|\[123, 234\]|报警联系人分组ID，格式为JSONArray。 |
|IsAutoStart|Boolean|否|true|生成报警规则后是否自动启动报警规则。默认为`false`。

 -   `true`：自动启动报警规则
-   `false`：不自动启动报警规则 |
|TemplageAlertConfig|String|否|\[ \{ "contactGroupIds": "381", "alertType": 5, "alarmContext": \{ "subTitle": "", "content": "报警名称：$报警名称\\n筛选条件：$筛选\\n报警时间：$报警时间\\n报警内容：$报警内容\\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！" \}, "alertLevel": "WARN", "metricParam": \{ "appId": "70901", "pid": "atc889zkcf@d8deedfa9bf\*\*\*\*", "type": "TXN", "dimensions": \[ \{ "type": "STATIC", "value": "\\\\/hello\_test\_api\_address\\\\/test1", "key": "rpc" \} \] \}, "alertWay": \[ "SMS", "MAIL", "DING\_ROBOT" \], "alertRule": \{ "rules": \[ \{ "measure": "appstat.txn.rt", "alias": "入口调用响应时间\_ms", "aggregates": "AVG", "nValue": 1, "value": 1, "operator": "CURRENT\_GTE" \} \], "operator": "\|" \}, "title": "报警模板报警名", "config": "\{\\"continuous\\":false,\\"dataRevision\\":2,\\"ownerId\\":\\”123412341234\\"\}", "notice": \{ "noticeStartTime": 1480521600000, "startTime": 1480521600000, "endTime": 1480607940000, "noticeEndTime": 1480607940000 \}, "status": "NON” \} \]|ARMS报警规则的配置JSON串。**TemplateAlertId**和**TemplageAlertConfig**必须至少填写一个。如果两个参数都填写，则**TemplateAlertId**优先。关于此字段的详细说明参见下文**关于参数TemplageAlertConfig的补充说明**。 |

## 关于参数**TemplageAlertConfig**的补充说明

**如何在ARMS控制台生成报警模板JSON串**

1. 在ARMS控制台的**报警管理 \> 报警策略管理**页面创建一个应用监控报警作为模板。

2. 在**报警管理 \> 报警策略管理**页面上选中此报警，并单击页面底部的**批量导出报警**。

3. 在**报警规则导出**对话框中复制ARMS生成的报警模板JSON串。

**JSON串示例及说明**

```

[
  {

    "contactGroupIds": "381",                         // 报警通知发送的联系人分组ID，以半角逗号（,）分隔。报警模板中忽略，导入时会映射对应值。
    "alertType": 5,                                   // 可选值为4和5。4表示前端监控报警，5表示应用监控报警。
    "alarmContext": {                                 // 报警通知内容模板。
      "subTitle": "",
      "content": "报警名称：$报警名称\n筛选条件：$筛选\n报警时间：$报警时间\n报警内容：$报警内容\n注意：该报警未收到恢复邮件之前，正在持续报警中，24小时后会再次提醒您！"
    },
    "alertLevel": "WARN",                             // 报警等级：FATAL、ERROR、WARN。
    "metricParam": {
      "appId": "70901",                               // 报警关联的应用AppId。模板报警配置中可随意填写，导入时会映射对应值。
      "pid": "atc889zkcf@d8deedfa9bf****",            // 报警关联的应用Pid。模板报警配置中可随意填写，导入时会映射对应值。
      "type": "TXN",                                  // 报警指标类型，详见下一节。
      "dimensions": [                                 // 报警关联的维度，详见下一节。
        {
          "type": "STATIC",
          "value": "\/hello_test_api_address\/test1",
          "key": "rpc"
        }
      ]
    },
    "alertWay": [                                       // 报警通知发送方式：SMS（开启短信通知）、MAIL（开启邮件通知）、DING_ROBOT（开启钉钉机器人通知）。
      "SMS",
      "MAIL",
      "DING_ROBOT"
    ],
    "alertRule": {
      "rules": [                                          // 报警判断规则列表
        {
          "measure": "appstat.txn.rt",                    // 报警规则请求指标，详见下一节。
          "alias": "入口调用响应时间_ms",                 // 报警规则请求指标展示字段，报警模板无需填此字段。
          "aggregates": "AVG",                            // 数据请求后聚合算子。AVG为取平均，SUM为取和，MIN为取最小值，MAX为取最大值。
          "nValue": 1,                                    // 报警规则每分钟轮询请求几分钟的数据。
          "value": 1,                                     // 报警规则判断阈值。
          "operator": "CURRENT_GTE"                       // CURRENT_GTE：大于或等于；CURRENT_LTE：小于或等于；PREVIOUS_UP：环比上升；PREVIOUS_DOWN：环比下降；HOH_UP：与上小时同比上升；HOH_DOWN：与上小时同比下降；DOD_UP：与昨日同比上升百分比；DOD_DOWN：与昨日同比下降百分比。
        }
      ],
      "operator": "|"                                     // 表示多个判断条件的组合方式。&为与逻辑，|为或逻辑。
    },
    "title": "报警模板报警名",                              // 模板报警名称。导入后，会生成新报警名称“{title}-应用名”。
    "config": "{\"continuous\":false,\"dataRevision\":2,\"ownerId\":\”123412341234\"}",          // continuous为true表示连续报警，continuous为false表示以24小时为静默期的静默报警策略。dataRevision字段为数据修订策略，0表示补零，1表示补1，2表示空值，即不处理。
    "notice": {                                                                                  // unix timstamp ms时间戳，noticeStartTime与noticeEndTime时间戳表示通知时间范围，startTime与endTime表示报警生效时间范围，timestamp转换为时间戳表示当天时间点，如1565964097071对应2019-08-16 22:01:37。
      "noticeStartTime": 1480521600000,
      "startTime": 1480521600000,
      "endTime": 1480607940000,
      "noticeEndTime": 1480607940000
    },
    "status": "NON”                                        // 报警当前启动状态。报警模板中忽略此字段，导入时会映射对应值。
  }
]

```

**关于报警模板中Measure、Dimension、metricParam.type的说明**

每个报警属于一个类型（type），由**metricParam.type**字段控制。每类报警都能设置一种维度（Dimension）作为筛选条件。每类报警都可以配置多个报警规则（alertRule），每个**alertRule**可以配置多个属于此类型的数据请求指标进行计算。

**Dimensions.type**包含以下可选值：

-   `STATIC`： 固定匹配此维度值需要填**dimensions.value**。
-   `ALL`：遍历所有维度值，按此接口所有接口名的指标依次判断，哪个接口触发阈值引起报警，就会在报警内容中体现该接口名，此时不需要填**dimensions.value**。
-   `DISABLE`：聚合所有维度值为一个值（求和），此时不需要填**dimensions.value**。

**报警指标取值枚举**

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

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|\[12174\*\*\]|报警规则ID |
|RequestId|String|A5EC8221-08F2-4C95-9AF1-49FD998C\*\*\*\*|请求ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ImportAppAlertRules
&ContactGroupIds=[123, 234]
&Pids=["atc889zkcf@d8deedfa9bfxxxx", "acd129bfcf@d5daebfa6cdxxxx"]
&RegionId=cn-hangzhou
&TemplateAlertId=324324234
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ImportAppAlertRulesResponse>
      <RequestId>A5EC8221-08F2-4C95-9AF1-49FD998C****</RequestId>
      <Data>[12174**]</Data>
</ImportAppAlertRulesResponse>
```

`JSON`格式

```
{
    "RequestId": "A5EC8221-08F2-4C95-9AF1-49FD998C****",
    "Data": "[12174**]"
}
```

