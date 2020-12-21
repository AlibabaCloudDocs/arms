# Custom configuration

Some common settings of application monitoring, such as the sampling rate of traces, agent switch, and slow SQL threshold, can be directly configured on the Custom Configuration tab.

[Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.

2.  On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the **Custom Configuration** tab.

4.  Configure the custom parameters and click **Save** in the lower part of the page.


## Configure trace sampling settings

In the **Invocation Trace Sampling Settings** section, you can turn on or off the sampling, and set the sampling rate. You need to enter only the number of the percentile in the **Sampling Rate Settings** field. For example, if you enter 10, the sampling rate is 10%.

**Note:** The modification takes effect immediately. You do not need to restart the application. If sampling is turned off, the trace data is not captured. Proceed with caution.

![Chain sampling](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9549558061/p169596.png)

## Configure the agent switch and log level

In the **Agent Switch Settings** section, you can turn on or off the probe master switch and other plug-in switches, and configure the log level.

**Note:** The modifications to the master switch of the agent and log level take effect immediately and do not require you to restart the application. If the master switch of the agent is turned off, Application Real-Time Monitoring Service \(ARMS\) cannot monitor your applications. Proceed with caution. To make changes to each plug-in switch take effect, you must manually restart the application.

![Agent Switches](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1652458061/p43148.png)

## Configure threshold settings

In the **Threshold Settings** section, you can set the slow SQL query threshold, interface response time threshold, and throttling threshold.

![Threshold Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2652458061/p43149.png)

## Configure advanced settings

In the **Advanced Settings** section, you can set the interface to be filtered and the maximum length of the method stack.

![Advanced Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2652458061/p43183.png)

-   **Invalid Interface Invocation Filtering**: Enter an interface whose call status does not need review. Then, this interface is hidden from the Interface Invocation page.
-   **Method stack maximum length**: Default value: 128. Maximum value: 400. Unit: entry.
-   **Stack Depth to Distinguish Exceptions**: The stack depth that is used to distinguish exceptions of a same type. This parameter is typically set to the call depth of the first difference.
-   **Collect the maximum length of SQL**: Default value: 1024. Minimum value: 256. Maximum value: 4096. Unit: character.
-   **Capture SQL Bound Variables**: Specifies whether to capture the variable value bound with PrepareStatement. This parameter takes effect without restarting the application.
-   **Original SQL**: SQL statements are only truncated.
-   **Exception Filtering**: The exception that you enter is not displayed in the chart on the Application Details and Exception Analysis tabs.
-   **Errors Filtering**: By default, HTTP status codes greater than 400 are counted as errors. You can specify the error codes that are greater than 400 but that you do not want to be counted as errors.
-   **New Trace Format**: Specifies whether to use a new storage format that sort traces by time. This parameter is enabled by default.
-   **Trace Compression**: Specifies whether to simplify duplicated calls such as for loops. This parameter takes effect without restarting the application.
-   **Maximum Request Parameter Length**: Default value: 512. Maximum value: 2048. Unit: character.
-   **Show Percentiles**: Specifies whether to turn on quantile statistics.
-   **Enable application emergency alert**: Specifies whether to enable alerts for emergencies such as thread deadlocks and out-of-memory \(OOM\). The [agent version](/intl.en-US/Application monitoring/Reference/Versions of the ARMS agent.md) must be 2.5.8 or later.
-   **RabbitMQ Consumer**: Specify the class name of a consumer or the name of the class that contains an anonymous internal consumer. You can then view the trace of the customer. Separate multiple names with commas \(,\).

## Configure thread settings

In the **Thread Settings** section, you can enable or disable thread diagnosis method stack and thread profiling master. You can also set the trigger threshold of the slow call listener.

![Thread Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2652458061/p43185.png)

**Note:** The listener is started only when the service call response time exceeds the threshold \(1,000 ms by default\) and lasts until the call ends or the consumed time exceeds 15 seconds. We recommend that you set the threshold to the 99th percentile of the call response time. For example, if 100 calls are listed in ascending order by response time, the time consumed by the 99th one is the 99th percentile.

## Configure memory snapshot settings

In the **Memory Snapshot Settings** section, you can enable or disable memory snapshots. If you enable it, a memory dump \(at most one time a day\) is created when memory leaks occur.

![Memory Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2652458061/p46550.png)

## Associate a business log with the trace ID

In the **Business Log Association Settings** section, you can set whether to associate the business log of an application with the trace ID. For more information, see [Associate the trace ID of a trace with business logs]().

![Business log](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5762658061/p22045.png)

## Configure URL convergence rules

In the **URL Convergence Settings** section, you can enable or disable the convergence feature. You can also set the convergence threshold, convergence rules and troubleshooting rules. URL convergence means that similar URLs are displayed together as a single object. For example, URLs prefixed with /service/demo are displayed as an object. The convergence threshold is the minimum number of URLs to trigger URL convergence. For example, when the threshold is 100, URLs converge only when 100 URLs meet the regular expression of the rules.

![URL Aggregation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5762658061/p46552.png)

## Business monitoring settings

In the **Business Monitoring Settings** section, you can enable or disable business monitoring and configure HTTP encoding.

![Business monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5762658061/p169619.png)

**Related topics**  


[Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md)

[API monitoring](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md)

[Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Use ARMS TProf to analyze code problems.md)

[Memory snapshot](/intl.en-US/Application monitoring/Features provided by the console/Application details/Memory snapshot.md)

