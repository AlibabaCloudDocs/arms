---
keyword: [ARMS, trace]
---

# Use trace sampling policies

This topic describes a variety of trace sampling policies that are supported by Application Real-Time Monitoring Service \(ARMS\). You can select appropriate trace sampling policies based on your scenarios so that you can obtain the desired trace data at a low cost.

Trace sampling is suitable for high-traffic applications that have a large number of visits. Trace sampling can help you record the most valuable trace data at a low cost and a low performance overhead. The basic principle of trace sampling is to preferentially record the traces that you are most concerned about and most likely to access. ARMS provides the following trace sampling policies:

-   [Trace feature-based sampling](#section_kmi_ene_r6n)
-   [Business feature-based sampling](#section_iso_yj4_qal)
-   [O&M feature-based sampling](#section_es1_yx3_lpz)
-   [Time feature-based sampling](#section_vqn_lfq_8e2)

**Note:** You can use the preceding trace sampling policies in combination to fully meet your personalized sampling requirements.

## Trace feature-based sampling

Trace feature-based sampling refers to the sampling based on the attributes of traces, such as time consumption and status. ARMS supports fixed-rate sampling and sampling based on thread profiling for slow calls.

Fixed-rate sampling records a specific proportion of trace data based on the ordinal number of TraceId. For example, if the fixed rate is 10%, one out of every 10 pieces of trace data is recorded. Fixed-rate sampling avoids incomplete trace data. The data of an entire trace is retained or discarded.

Fixed-rate sampling applies to the following scenarios:

-   During the peak hours of stress testing or big promotions, the traffic volume is high. If full trace logs are reported, the client performance may be degraded. To avoid this situation, we recommend that you reduce the fixed sample rate 1% to 10%.
-   On regular days, the cost of network bandwidth is high because full trace logs are reported. In this case, you can consider adjusting the fixed sample rate as needed.

The following figure shows how fixed-rate sampling works.

![dg_part](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8867458061/p201538.png)

You can perform the following steps to configure fixed-rate sampling:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.

3.  On the Applications page, click the name of the application.

4.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the **Custom Configuration** tab.

5.  In the **Invocation Trace Sampling Settings** section, turn on or turn off the switch of trace sampling and specify a sample rate. In the **Sampling Rate Settings** field, you need only to enter the number of the percentile. For example, if you enter 10, the sample rate is 10%.

    **Note:** The modification takes effect immediately. You do not need to restart the application. If sampling is turned off, the trace data is not captured. Proceed with caution.

    ![Chain sampling](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9549558061/p169596.png)


Sampling based on thread profiling for slow calls records data of traces in which thread profiling is triggered to listen on slow calls. After thread profiling is enabled, ARMS transfers a sampling mark to the downstream at the same time when ARMS records a slow call. ARMS also retains the downstream traces of this slow call. However, the number of listening threads of thread profiling is limited to avoid compromised client performance. If multiple slow calls occur at the same time, only some slow calls that meet the conditions and their downstream traces are recorded.

Sampling based on thread profiling for slow calls applies to the following scenarios:

-   The system encounters occasional slow calls. For example, the response time of services surges from 0.5s to 10s at night. Assume that you enable thread profiling in advance \(the default trigger threshold is 2s\). ARMS automatically records the native method stacks of slow calls that are completed within 2s to 10s in the request and the downstream traces of the slow calls.
-   The system responds at a slow speed during the peak hours of flash sales or periodic big promotions. In this case, thread profiling records the native method stacks of slow calls that reach the trigger threshold and the downstream traces of the slow calls.

The following figure shows how sampling based on thread profiling for slow calls works.

![dg_slow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9867458061/p201537.png)

You can perform the following steps to configure sampling based on thread profiling for slow calls:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.

3.  On the Applications page, click the name of the application.

4.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the **Custom Configuration** tab.

5.  In the **Thread settings** section, turn on or turn off the switch of the thread diagnostics method stack and the master switch of thread profiling. Specify a threshold to trigger slow call listening.

    ![Thread Settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2652458061/p43185.png)

    **Note:** The listener is started only when the service call response time exceeds the threshold \(1,000 ms by default\) and lasts until the call ends or the consumed time exceeds 15 seconds. We recommend that you set the threshold to the 99th percentile of the call response time. For example, if 100 calls are listed in ascending order by response time, the time consumed by the 99th one is the 99th percentile.




## Business feature-based sampling

Business feature-based sampling refers to the sampling based on the business traffic features of applications. ARMS allows you to configure rules based on the HTTP traffic features of entry applications. You can filter Header, Method, Cookie, and Parameter information when you extract business features so that the conditions for matching business features can be met in various scenarios. After the switch of full collection is turned on, the trace data that meets the business conditions can be fully collected in priority. The configuration immediately takes effect, and can be dynamically modified during runtime.

Business feature-based sampling applies to the following scenarios:

The following figure shows how business feature-based sampling works.

![dg_scenario](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9867458061/p200647.png)

You can perform the following steps to configure sampling based on business features:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the Basic information section on the New business monitoring page, specify the following information. Click **Advanced Settings**. In the Advanced Settings section, specify the following information. Then, click **Save**.

    ![pg_business](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0649558061/p200646.png)

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |**Business Name**|The name of the business monitoring job. This parameter is required.|Business feature test.|
    |**Entry application**|In the **Entry application** list, all the Java applications that have application monitoring agents installed appear. This parameter is required. After you select the required application, ARMS automatically detects the version number of the application agent. **Note:** You can use the business monitoring feature only after you upgrade the application agent to a version later than 2.6.2. If the detected agent version is not later than 2.6.2, upgrade the agent first. For more information, see [Preparations]().

|mall-center.|
    |**Service type**|Set the service type. This parameter is required. ARMS supports only **HTTP entry**. This service type is suitable for scenarios where business traces are dyed based on HTTP traffic features.|**HTTP entry**.|
    |**Service name**|The API name that is provided by the application. This parameter is required. ARMS automatically detects a list of APIs that are recently provided by this application based on the **Entry application** you specify for your choices. If the recommended APIs do not meet your requirements, you can edit the APIs. The following four types of matching patterns of **Service name** are supported:

    -   **Equal**: exactly matches the business API of **Service name**. This pattern is the default matching pattern.
    -   **Start equal**: matches the business APIs that are prefixed with **Service name**. If you need to monitor the business APIs that have the same prefix, select this pattern.
    -   **Contains**: matches the business APIs that contain **Service name**. If your application provides a large number of business APIs, you can select this pattern to quickly monitor the business APIs that you need.
    -   **End =**: matches the business APIs that are suffixed with **Service name**. This pattern is suitable for typical web frameworks that end with the .do and .action configurations.
    -   **Pattern matching**: matches dynamic URI paths and supports matching rules for Ant-style path patterns. This allows you to monitor and analyze the URIs of a specific type of patterns.
|**Equal** /api/buy.|
    |**Filtering rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|**Meet the following rules at the same time**.|
    |**Filter rules**|Further filter the business APIs that you specify. This parameter is optional. To specify **Filter rules**, you must specify a parameter to be matched \(**Parameter**, **Cookie**, **Method**, **PathVariable**, and **Header**\), a key value to be matched, and a matching pattern \(**==**, **!=**, and **contains**\), and a threshold. Among the preceding information, the **PathVariable** option appears for the parameter to be matched only if you select **Pattern matching** for **Service name** and the input string includes the brace \(\{\}\) placeholders. You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filtering rule relationships** you specify.|Assume that your application provides the /api/buy? brand=\*\*\* URL and you want to monitor the API operations of brand=Alibaba. You can set **Filter rules** to **Parameter** brand **==** Alibaba in the form.|
    |**Whether full collection**|Specifies whether to collect all the traces that have dye labels.|Yes.|


## O&M feature-based sampling

O&M feature-based sampling refers to the sampling based on the O&M features of applications, such as the deployment environment and the network environment. ARMS supports sampling based on the Kubernetes Pod Metadata characteristics of applications. ARMS allows you to configure O&M feature rules based on the Kubernetes Pod Metadata characteristics of entry applications. ARMS can automatically identify the metadata information of pod instances of applications, such as the label, annotation, pod name, and namespace, and filter the metadata information. This meets the conditions for matching O&M features in various scenarios. After the switch of full collection is turned on, the trace data that meets the O&M feature conditions can be fully collected in priority. The configuration immediately takes effect, and can be dynamically modified during runtime.

O&M feature-based sampling applies to the following scenarios:

-   Specific sampling settings are required based on the difference of information about application agents, such as languages, versions, environment variables, and startup parameters.
-   Specific sampling settings are required based on the difference of information about servers where applications are deployed, such as specifications, models, regions, and zones.
-   Specific sampling settings are required based on the difference of application deployment environments, such as the development, testing, pre-release, and production isolation requirements.
-   Specific sampling settings are required based on the difference between deployment modes of network environments where applications reside, such as physical machines, virtual machines, and containers. Alternatively, specific sampling settings are required based on the difference between the classic network and a VPC.

The following figure shows how O&M feature-based sampling works.

![dg_k8s_ts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9867458061/p200585.png)

You can perform the following steps to configure O&M feature-based sampling:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the Basic information section on the New business monitoring page, specify the following information. Click **Advanced Settings**. In the Advanced Settings section, specify the following information. Then, click **Save**.

    ![pg_k8s](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0649558061/p200636.png)

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |**Business Name**|The name of the business monitoring job. This parameter is required.|O&M feature test.|
    |**Entry application**|In the **Entry application** list, all the Java applications that have application monitoring agents installed appear. This parameter is required. After you select the required application, ARMS automatically detects the version number of the application agent. **Note:** You can use the business monitoring feature only after you upgrade the application agent to a version later than 2.6.2. If the detected agent version is not later than 2.6.2, upgrade the agent first. For more information, see [Preparations]().

|product-center.|
    |**Service type**|Set the service type. This parameter is required. ARMS supports only **Kubernetes Pod Metadata**. This service type is suitable for scenarios where business traces are dyed based on the environment characteristics of Kubernetes pods.|**Kubernetes Pod Metadata**.|
    |**Filtering rule relationships**|You can select **Meet the following rules at the same time** or **Meet the following rule**.|**Meet the following rules at the same time**.|
    |**Filter rules**|Further filter the business APIs that you specify. This parameter is optional. To specify **Filter rules**, you must specify a parameter to be matched \(**podLabel**, **podAnnotation**, **podName**, **podNamespace**, **podUID**, **podIp**, **nodeName**, **hostIp**, and **podServiceAccount**\), a matching pattern \(**==**, **!=**, and **contains**\), and a threshold. You can set multiple filter rules. The logical relationship between multiple filter rules is determined by the **Filtering rule relationships** you specify.|Assume that your application is deployed in the environments, such as dev, test, stagging, and prod. The Pod label stge label is used for environment differentiation. You want to monitor the dev environment and collect all traces. In this case, you can set **Filter rules** to **podLabel** stage **==** dev in the form.|
    |**Whether full collection**|Specifies whether to collect all the traces that have dye labels.|Yes.|


## Time feature-based sampling

Time feature-based sampling refers to the sampling based on the time features of applications, such as online diagnostics and offline analysis. Requirements on sample rates vary based on diagnostic scenarios. ARMS supports temporary full collection in online diagnostic scenarios and helps you quickly locate online problems. After real-time diagnosis is enabled, ARMS continuously monitors the application for 5 minutes and reports all the trace data during this period. Then, you can start from the trace that has performance problems, and use features, such as the waterfall charts of method stacks and thread profiling, to identify the causes of the problems.

Time feature-based sampling applies to the following scenarios:

You need to closely monitor the application performance for a short period of time, for example, when you release an application or perform stress testing on the application.

The following figure shows how time feature-based sampling works.

![dg_temp](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9867458061/p201540.png)

You can perform the following steps to configure time feature-based sampling:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region in the top navigation bar.

3.  On the Applications page, click the name of the application.

4.  In the left-side navigation pane, choose **Application Diagnosis** \> **Real-time Diagnosis**.

    The first time you go to the Real-time Diagnosis page, real-time diagnosis is automatically enabled by default. To enable real-time diagnosis in other cases, click **Activate Real-time Diagnosis** in the upper-right corner of the page.

    Real-time diagnosis is automatically disabled after it is automatically enabled for 5 minutes. To early disable real-time diagnosis, click **Pause Auto-Refresh** in the upper-right corner of the page.


