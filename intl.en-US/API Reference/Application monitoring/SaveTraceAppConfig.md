# SaveTraceAppConfig

Customizes application monitoring settings, such as trace sampling and agent switch settings.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=ARMS&api=SaveTraceAppConfig&type=RPC&version=2019-08-08)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SaveTraceAppConfig|The operation that you want to perform. Set the value to SaveTraceAppConfig. |
|Pid|String|Yes|a2n80plglh@745eddxxx|The process identifier \(PID\) of the application. For more information, see [Obtain the PID of an application](https://www.alibabacloud.com/help/zh/doc-detail/186100.htm?spm=a2cdw.13409063.0.0.7a72281f0bkTfx#title-imy-7gj-qhr). |
|Settings.N.Key|String|No|sampling.enable|The key in the setting that you want to customize. For more information about the supported settings, see the following sections.

-   Trace sampling setting
-   Main switch setting
-   Threshold setting
-   Advanced setting
-   Thread setting
-   Memory snapshot setting
-   URL convergence setting
-   Business log association setting
-   Business monitoring setting |
|Settings.N.Value|String|No|true|The value in the setting that you want to customize. For more information about the supported settings, see the following sections.

-   Trace sampling setting
-   Main switch setting
-   Threshold setting
-   Advanced setting
-   Thread setting
-   Memory snapshot setting
-   URL convergence setting
-   Business log association setting
-   Business monitoring setting |
|RegionId|String|No|cn-hangzhou|The ID of the region. |

**Keys in the trace sampling setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|sampling.enable

|Specifies whether to turn on the sampling switch.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch. |
|sampling.rate

|The sampling rate.

|Value range: 0 to 100. Default value: 10. |

**Key in the main switch setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|enable

|Specifies whether to turn on the main switch of the ARMS agent.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch. |

**Keys in the threshold setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|thresholds.limit

|The throttling threshold.

|Default value: 100. |
|thresholds.interface

|The response time threshold of API calls.

|Default value: 500. Unit: milliseconds. |
|thresholds.sql

|The threshold of the time consumed for slow SQL queries.

|Default value: 500. Unit: milliseconds. |

**Keys in the advanced setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|defined.excludeurl

|The filter of invalid API calls.

|Separate multiple APIs with commas \(,\). Example: /service/taobao,/service/status. |
|callstack.maxLength

|The threshold of the maximum stack length.

|Default value: 128. The maximum stack length allowed is 400. |
|callsql.maxLength

|The maximum length of collected SQL statements.

|A collected SQL statement must be 256 to 4096 characters in length. Default value: 1024. |
|exception.whitelist

|The filter of exceptions.

|The value must be a regular expression that specifies the name of an exception category. Separate multiple expression categories with commas \(,\). Example: java.lang.InterrupetedException,java.lang.IndexOutOfBoundsException. The exceptions of the categories that you specify are not displayed in the chart on the Application Details and Exceptions Diagnosis pages. |
|error.skip

|The filter of errors.

|By default, all HTTP status codes greater than 400 are counted as errors. To ignore specific HTTP status codes greater than 400 so that they are not counted as errors, you can specify them in value. Separate multiple HTTP status codes with commas \(,\). Examples: 429 and 429,512. This key is supported by the ARMS agent V2.5.7.2 or later. |

**Keys in the thread setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|tprof.enableThreadProfiler

|Specifies whether to turn on the main switch of thread profiling.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch.

If you turn on this switch, the native method stacks of slow API calls are automatically saved. |
|tprof.threadProfilerSlowInteractionRt

|The threshold of the time consumed for slow API calls.

|Default value: 2000. If the time consumed for slow API calls exceeds the threshold, thread profiling is enabled. We recommend that you set the value to the 99th percentile of the consumed time. If you set a value smaller than 2000, the CPU consumption is increased. We recommend that you set a value greater than or equal to 500. |
|tprof.enableThreadStackRecorder

|Specifies whether to enable the thread diagnostics method stack.

|Valid values:

- `true`: enables the thread diagnostics method stack.

- `false`: disables the thread diagnostics method stack.

If you enable this feature, the method stack is collected every 5 minutes. |

**Key in the memory snapshot setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|mprof.isEnableLeakDump

|Specifies whether to turn on the memory snapshot switch.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch.

If you turn on this switch, the memory is automatically dumped at most once a day when memory leaks occur. |

**Keys in the URL convergence setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|convergence.enable

|Specifies whether to enable the URL convergence feature.

|Valid values:

- `true`: enables the URL convergence feature.

- `false`: disables the URL convergence feature. |
|convergence.minServerSize

|The convergence threshold.

|If the threshold is exceeded, convergence is enabled. |
|convergence.pattern

|The regular expression of convergence rules.

|You can use regular expressions to configure convergence rules. Separate multiple regular expressions with commas \(,\). Enter a URL in the original text to indicate that the URL is not converged. Example: /service/\(.\\\*?\)/demo. |

**Keys in the business log association setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|logging.enable

|Specifies whether to turn on the switch that associates trace IDs with business logs.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch.

If you turn on this switch, trace IDs are automatically generated in the business logs of an application. This setting takes effect after you restart the application. Logging utilities such as Log4j, Log4j2, and Logback are supported. You must add %X\{EagleEye-TraceID\} to the log layout to generate trace IDs. |
|SLS.project

|The Log Service project that stores the business logs generated in the current region.

|You can specify the name of the Log Service project that stores the business logs generated in the current region. |
|SLS.logStore

|The Log Service Logstore that stores the business logs generated in the current region.

|You can specify the name of the Log Service Logstore that stores the business logs generated in the current region. |

**Keys in the business monitoring setting**

|Key

|Description

|Value |
|-----|-------------|-------|
|scenario.enable

|Specifies whether to turn on the business monitoring switch.

|Valid values:

- `true`: turns on the switch.

- `false`: turns off the switch.

This key specifies whether business monitoring takes effect. This key is supported by the ARMS agent V2.6.2 or later. |
|scenario.http.encoding

|The HTTP encoding format.

|This key specifies how to parse HTTP parameters. Default value: UTF-8. You can specify an encoding format as needed. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Data|String|success|Indicates whether the request was successful. |
|RequestId|String|78901766-3806-4E96-8E47-CFEF59E4\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SaveTraceAppConfig
&Pid=a2n80plglh@745eddxxx
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

