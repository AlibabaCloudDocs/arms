# SaveTraceAppConfig

调用SaveTraceAppConfig接口进行应用监控的自定义设置（如调用链采样设置、Agent开关等）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=SaveTraceAppConfig&type=RPC&version=2019-08-08)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SaveTraceAppConfig|系统规定参数。取值：SaveTraceAppConfig。 |
|Pid|String|是|a2n80plglh@745eddxxx|应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr)。 |
|Settings.N.Key|String|否|sampling.enable|自定义设置，各设置的详细字段见下文说明。

 -   调用链路采样相关
-   总开关设置
-   阈值设置
-   高级设置
-   线程设置
-   内存快照设置
-   URL收敛设置
-   业务日志关联设置
-   业务监控设置 |
|Settings.N.Value|String|否|true|自定义设置，各设置的详细字段见下文说明。

 -   调用链路采样相关
-   总开关设置
-   阈值设置
-   高级设置
-   线程设置
-   内存快照设置
-   URL收敛设置
-   业务日志关联设置
-   业务监控设置 |
|RegionId|String|否|cn-hangzhou|地域ID。 |

**调用链路采样字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|sampling.enable

|采样开关

|取值：

 - `true`：开启采样开关。

 - `false`：关闭采样开关。 |
|sampling.rate

|采样率

|0~100之间，默认为10。 |

**总开关字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|enable

|Agent总开关

|取值：

 - `true`：开启Agent总开关。

 - `false`：关闭Agent总开关。 |

**阈值字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|thresholds.limit

|限流阈值

|默认为100。 |
|thresholds.interface

|接口响应时间阈值

|默认为500，单位为ms。 |
|thresholds.sql

|慢SQL查询阈值

|默认为500，单位为ms。 |

**高级字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|defined.excludeurl

|无效接口调用过滤

|支持以英文逗号（,）分隔多个接口调用。示例：/service/taobao,/service/status。 |
|callstack.maxLength

|方法堆栈最大长度间阈值

|默认为128，支持最大长度400条。 |
|callsql.maxLength

|采集SQL最大长度

|默认为1024个字符，最小长度为256个字符，最大长度为4096个字符。 |
|exception.whitelist

|异常过滤

|使用正则表达式匹配异常类全名，多个异常请使用英文逗号（,）分隔。例如：java.lang.InterrupetedException,java.lang.IndexOutOfBoundsException。此处输入的异常不会显示在应用详情和异常分析页面的图表中。 |
|error.skip

|错误数过滤

|默认情况下，大于400的状态码会计入错误数，您可以设置需要忽略的状态码，多个错误码使用英文逗号（,）分隔，例如：429或429,512。Agent 2.5.7.2以上版本支持。 |

**线程字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|tprof.enableThreadProfiler

|线程剖析总控开关

|取值：

 - `true`：开启线程剖析总控开关。

 - `false`：关闭线程剖析总控开关。

 开启后自动保存慢调用本地方法栈。 |
|tprof.threadProfilerSlowInteractionRt

|慢调用监听触发阈值

|默认为2000。耗时高于该阈值才启动线程剖析，建议设为耗时的99分位线。低于2000ms会增加CPU消耗，不可小于500ms。 |
|tprof.enableThreadStackRecorder

|线程诊断方法栈

|取值：

 - `true`：开启线程诊断方法栈。

 - `false`：关闭线程诊断方法栈。

 开启后每隔5分钟采集一次方法栈。 |

**内存快照字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|mprof.isEnableLeakDump

|内存快照开关

|取值：

 - `true`：开启内存快照开关。

 - `false`：关闭内存快照开关。

 开启后出现内存泄露将自动Dump内存，一天最多一次。 |

**URL收敛字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|convergence.enable

|收敛URL

|取值：

 - `true`：开启收敛URL。

 - `false`：关闭收敛URL。 |
|convergence.minServerSize

|收敛阈值

|大于此阈值即进行收敛。 |
|convergence.pattern

|收敛规则正则

|可使用正则表达式设置收敛规则，多个正则表达式之间以英文逗号（,）分隔，直接填写URL原文表示不收敛此URL，例如：/service/\(.\\\*?\)/demo。 |

**业务日志关联字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|logging.enable

|关联业务日志与TraceId开关

|取值：

 - `true`：开启关联业务日志与TraceId开关。

 - `false`：关闭关联业务日志与TraceId开关。

 开启后业务日志中会自动生成调用链的TraceId，此设置在重启应用后生效。支持Log4j/Log4j2/Logback日志组件。业务应用需要在日志的Layout中通过声明%X\{EagleEye-TraceID\}来输出TraceId信息。 |
|SLS.project

|当前区域业务日志的project

|当前区域业务日志的project。 |
|SLS.logStore

|当前区域业务日志的logstore

|当前区域业务日志的logstore。 |
|SLS.index

|当前区域业务日志的关联索引

|取值：

 -   当指定全文索引时，不传。
-   指定字段索引时，取值为相应的字段名。例如：**SLS.index: tag**。

 字段索引及全文索引的区别，请参见[配置索引](~~90732~~)。 |

**业务监控字段说明**

|Key

|字段说明

|Value |
|-----|------|-------|
|scenario.enable

|业务监控开关

|取值：

 - `true`：开启业务监控开关。

 - `false`：关闭业务监控开关。

 控制业务监控是否生效，Agent 2.6.2以上版本支持。 |
|scenario.http.encoding

|HTTP编码

|默认为UTF-8，用于对HTTP参数解析，请按实际情况设置。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Data|String|success|操作是否成功。 |
|RequestId|String|78901766-3806-4E96-8E47-CFEF59E4\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SaveTraceAppConfig
&Pid=a2n80plglh@745eddxxx
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<SaveTraceAppConfigResponse>
      <RequestId>78901766-3806-4E96-8E47-CFEF59E4****</RequestId>
      <Data>success</Data>
</SaveTraceAppConfigResponse>
```

`JSON`格式

```
{
    "RequestId": "78901766-3806-4E96-8E47-CFEF59E4****",
    "Data": "success"
}
```

