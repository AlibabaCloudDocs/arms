# SaveTraceAppConfig

Customizes Application Monitoring settings, such as trace sampling and agent switch settings.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=QueryMetric&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Pid|String|Yes|xxx@74xxx|The identifier of the application. For more information, see [Obtain the PID of an application](/intl.en-US/API reference/Application monitoring/QueryMetricByPage (Application Monitoring).md). |
|Settings.N.Key|String|No|sampling.enable|The settings that you want to customize.-   [Configure trace sampling settings](#table_6hs_0c7_i8n)
-   [Configure main switch settings](#table_qib_r15_hya)
-   [Configure threshold settings](#table_2fd_pb3_j50)
-   [Configure advanced settings](#table_1wh_meh_gk2)
-   [Configure thread settings](#table_nhx_fo2_03u)
-   [Configure memory snapshot settings](#table_0gk_81r_1yg)
-   [Configure URL convergence settings](#table_8zz_lbb_4w5)
-   [Configure association log settings](#table_rzf_ylz_h0d)
-   [Configure business monitoring settings](#table_waq_hqt_0yq) |
|Settings.N.Value|String|No|true|
|RegionId|String|No|cn-hangzhou|The ID of the region.|

**Trace sampling fields**

|Key|Description|Value|
|---|-----------|-----|
|sampling.enable|The sampling switch.|-   true
-   false |
|sampling.rate|The sampling rate.|Value range: 0 to 100. Default value: 10.|

**Field of the main switch**

|Key|Description|Value|
|---|-----------|-----|
|enable|The agent switch.|-   true
-   false |

**Threshold fields**

|Key|Description|Value|
|---|-----------|-----|
|thresholds.limit|The throttling threshold.|Default value: 100.|
|thresholds.interface|The response time threshold of the API.|Default value: 5000. Unit: milliseconds.|
|thresholds.sql|The threshold of slow SQL queries.|Default value: 5000. Unit: milliseconds.|

**Fields of advanced settings**

|Key|Description|Value|
|---|-----------|-----|
|defined.excludeurl|The filter of invalid API calls.|You can use commas \(,\) to separate multiple APIs. Example:/service/taobao,/service/status.|
|callstack.maxLength|The threshold of the maximum stack length.|Default value: 128. The maximum stack length is 400.|
|callsql.maxLength|The maximum length of collected SQL statements.|A collected SQL statement must be 256 to 4096 characters in length. Default value: 1024.|

**Thread fields**

|Key|Description|Value|
|---|-----------|-----|
|tprof.enableThreadProfiler|The main switch of thread profiling.|-   true
-   false

If you turn on this switch, the native method stacks of slow API calls are automatically saved.|
|tprof.threadProfilerSlowInteractionRt|The threshold of the time consumed for slow API calls.|Default value: 2000.If the time consumed for slow API calls exceeds the threshold, thread profiling is enabled. We recommend that you set the value to the 99th percentile of the consumed time. If you set a value smaller than 2000, the CPU consumption is increased. We recommend that you set a value greater than or equal to 500. |
|tprof.enableThreadStackRecorder|The method stack of thread diagnosis.|-   true
-   false

If you enable this feature, the method stack is collected every 5 minutes.|

**Memory snapshot fields**

|Key|Description|Value|
|---|-----------|-----|
|mprof.isEnableLeakDump|The memory snapshot switch.|-   true
-   false

If you turn on this switch, the memory is automatically dumped at most once a day when memory leaks occur.|

**URL convergence fields**

|Key|Description|Value|
|---|-----------|-----|
|convergence.enable|The URL convergence.|-   true
-   false |
|convergence.minServerSize|The convergence threshold.|If the threshold is exceeded, convergence is enabled.|
|convergence.pattern|The regular expression of convergence rules.|You can use regular expressions to configure convergence rules. Separate multiple regular expressions with commas \(,\). Enter a URL in the original text to indicate that the URL is not converged. For example: /service/\(. \*?\) /demo.|

**Association logs fields**

|Key|Description|Value|
|---|-----------|-----|
|logging.enable|The switch that associates TraceId with business logs.|-   true
-   false

If you turn on this switch, the TraceId is automatically generated in the logs. This setting takes effect after you restart the application. Logging utilities such as Log4j, Log4j2, and Logback are supported. You must add % X\{EagleEye-TraceID\} to the log layout to generate the trace ID information.|
|SLS.project|The project that stores business logs generated in the current region.|The project that stores business logs generated in the current region.|
|SLS.logStore|The Logstore that stores business logs generated in the current region.|The Logstore that stores business logs generated in the current region.|

**Business monitoring fields**

|Key|Description|Value|
|---|-----------|-----|
|scenario.enable|The business monitoring switch.|-   true
-   false

Specifies whether business monitoring takes effect. This switch is supported by ARMS agent version 2.6.2 and later.|
|scenario.http.encoding|The HTTP encoding.|Specifies how to parse HTTP parameters. Default value: UTF-8. You can configure an encoding as needed.|

## Response parameters

|Parameter|Example|Description|
|---------|-------|-----------|
|RequestId|78901766-3806-4E96-8E47-CFEF59E4\*\*\*\*|The ID of the request.|
|data|success|Indicates whether the operation was successful.|

## Examples

Sample request

```
http(s)://[Endpoint]/? Action=SaveTraceAppConfig
&Pid=12334xxxxxxx343
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SaveTraceAppConfigResponse>
  <RequestId>78901766-3806-4E96-8E47-CFEF59E4****</RequestId>
  <Data>success</Data>
</SaveTraceAppConfigResponse>
```

`JSON` format

```
{
    "RequestId": "78901766-3806-4E96-8E47-CFEF59E4****",
    "Data": "success"
}
```

