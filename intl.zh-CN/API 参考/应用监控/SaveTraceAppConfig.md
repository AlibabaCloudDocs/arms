# SaveTraceAppConfig

调用SaveTraceAppConfig接口进行应用监控的自定义设置（如调用链采样设置、Agent开关等）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=QueryMetric&type=RPC&version=2019-08-08)

## 请求参数

|字段名称|字段类型|是否必选|示例值|描述|
|----|----|----|---|--|
|Pid|String|是|xxx@74xxx|应用的ID标识串。获取方式请参见[如何获取应用PID](https://www.alibabacloud.com/help/doc-detail/146244.htm#p-xyi-tr6-2w5)。 |
|Settings.N.Key|String|否|sampling.enable|选择需要自定义的设置。-   [调用链路采样相关](#table_6hs_0c7_i8n)
-   [总开关设置](#table_qib_r15_hya)
-   [阈值设置](#table_2fd_pb3_j50)
-   [高级设置](#table_1wh_meh_gk2)
-   [线程设置](#table_nhx_fo2_03u)
-   [内存快照设置](#table_0gk_81r_1yg)
-   [URL收敛设置](#table_8zz_lbb_4w5)
-   [业务日志关联设置](#table_rzf_ylz_h0d)
-   [业务监控设置](#table_waq_hqt_0yq) |
|Settings.N.Value|String|否|true|
|RegionId|String|否|cn-hangzhou|区域的ID。|

**调用链路采样字段说明**

|Key|字段说明|Value|
|---|----|-----|
|sampling.enable|采样开关|-   true
-   false |
|sampling.rate|采样率|0-100之间，默认为10。|

**总开关字段说明**

|Key|字段说明|Value|
|---|----|-----|
|enable|Agent总开关|-   true
-   false |

**阈值字段说明**

|Key|字段说明|Value|
|---|----|-----|
|thresholds.limit|限流阈值|默认为100。|
|thresholds.interface|接口响应时间阈值|默认为500，单位为ms。|
|thresholds.sql|慢SQL查询阈值|默认为500，单位为ms。|

**高级字段说明**

|Key|字段说明|Value|
|---|----|-----|
|defined.excludeurl|无效接口调用过滤|支持以英文逗号（,）分隔多个接口调用。示例：/service/taobao,/service/status。|
|callstack.maxLength|方法堆栈最大长度间阈值|默认为128，支持最大长度400条。|
|callsql.maxLength|采集SQL最大长度|默认为1024个字符，最小长度为256个字符，最大长度为4096个字符。|

**线程字段说明**

|Key|字段说明|Value|
|---|----|-----|
|tprof.enableThreadProfiler|线程剖析总控开关|-   true
-   false

开启后自动保存慢调用本地方法栈。|
|tprof.threadProfilerSlowInteractionRt|慢调用监听触发阈值|默认为2000。耗时高于该阈值才启动线程剖析，建议设为耗时的99分位线。低于2000ms会增加CPU消耗，不可小于500ms。 |
|tprof.enableThreadStackRecorder|线程诊断方法栈|-   true
-   false

开启后每隔5分钟采集一次方法栈。|

**内存快照字段说明**

|Key|字段说明|Value|
|---|----|-----|
|mprof.isEnableLeakDump|内存快照开关|-   true
-   false

开启后出现内存泄露将自动Dump内存，一天最多一次。|

**URL收敛字段说明**

|Key|字段说明|Value|
|---|----|-----|
|convergence.enable|收敛URL|-   true
-   false |
|convergence.minServerSize|收敛阈值|大于此阈值即进行收敛。|
|convergence.pattern|收敛规则正则|可使用正则表达式设置收敛规则，多个正则表达式之间以英文逗号（,）分隔，直接填写URL原文表示不收敛此URL，示例：/service/\(.\*?\)/demo。|

**业务日志关联字段说明**

|Key|字段说明|Value|
|---|----|-----|
|logging.enable|关联业务日志与TraceId开关|-   true
-   false

开启后业务日志中会自动生成调用链的TraceId，此设置在重启应用后生效。支持Log4j/Log4j2/Logback日志组件。业务应用需要在日志的Layout中通过声明%X\{EagleEye-TraceID\}来输出TraceId信息。|
|SLS.project|当前区域业务日志的project|当前区域业务日志的project。|
|SLS.logStore|当前区域业务日志的logstore|当前区域业务日志的logstore。|

**业务监控字段说明**

|Key|字段说明|Value|
|---|----|-----|
|scenario.enable|业务监控开关|-   true
-   false

控制业务监控是否生效，Agent 2.6.2以上版本支持。|
|scenario.http.encoding|HTTP编码|默认为UTF-8，用于对HTTP参数解析，请按实际情况设置。|

## 返回参数

|名称|示例值|描述|
|--|---|--|
|RequestId|78901766-3806-4E96-8E47-CFEF59E4\*\*\*\*|请求ID。|
|data|success|操作是否成功。|

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SaveTraceAppConfig
&Pid=12334xxxxxxx343
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SaveTraceAppConfigResponse>
  <RequestId>78901766-3806-4E96-8E47-CFEF59E4****</RequestId>
  <Data>success</Data>
</SaveTraceAppConfigResponse>
```

`JSON` 格式

```
{
    "RequestId": "78901766-3806-4E96-8E47-CFEF59E4****",
    "Data": "success"
}
```

