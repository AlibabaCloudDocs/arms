# Real-time diagnosis

The real-time diagnosis function provided by application monitoring of Application Real-Time Monitoring Service \(ARMS\) is suitable for scenarios that need close monitoring of application performance and location of the cause of problems within a short time. This topic describes how to use the real-time diagnosis function.

When you need to closely monitor the application performance for a short period of time, such as releasing an application or performing stress tests on the application, you can use the real-time diagnosis function of ARMS application monitoring. After real-time diagnosis is enabled, ARMS application monitoring continuously monitors the target application for five minutes and reports all data of the traces during this period. Next, you can use the method stack waterfall diagram and thread profiling to identify the causes of the exception based on the trace that shows performance problems.

## Portal

Follow these steps to go to ARMS application monitoring for real-time diagnosis.

1.  Log on to [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  On the Applications page, click the name of the target application.

4.  In the left-side navigation pane, click **Real-time Diagnosis**.


## Enable and disable real-time diagnosis

The first time you access the Real-time Diagnosis page, real-time diagnosis is automatically enabled. To enable real-time diagnosis in other cases, click **Enable real-time diagnosis** in the upper-right corner.

Real-time diagnosis is automatically started for five minutes and then disabled. To disable the real-time diagnosis in advance, click **Terminate Real-time Diagnosis** in the upper-right corner.

## View real-time monitoring data

In the **Real-time Requests Distribution** and **Requests by Response Time** sections, you can view the statistics of the last 1000 requests captured as of the current time point.

![Page Realtime Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54055.png)

In the chart of the **Real-time Requests Distribution** section, select a time range. Data of the selected time range can be set as visible. That is, the chart only displays data from this time range. Click **Reset** in the upper-right corner of the chart and the default view can be restored.

![Expanded Time Range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54056.png)

## Filter monitoring data

You can filter request monitoring data displayed on the page by interface name and IP address.

1.  Click the **+** icon at the top of the **Real-time Requests Distribution** section.

2.  Select an interface or IP from the drop-down list, and click **Query**.

    Only the request monitoring data of the selected interface is displayed on the page.


## View information of traces

On the **Traces** and **Interface Aggregation** tabs, you can view all information of the trace captured in the corresponding period. Click a TraceId to access the **Link Invocation** page. Use the local method stack waterfall diagram and thread profiling to locate the causes for the exception.

![Aggregated by API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54058.png)

For more information, see [Trace query](/intl.en-US/Application monitoring/Function specification/Trace query.md) and [Use ARMS TProf to analyze code problems](/intl.en-US/Application monitoring/Tutorials/Use ARMS TProf to analyze code problems.md).

