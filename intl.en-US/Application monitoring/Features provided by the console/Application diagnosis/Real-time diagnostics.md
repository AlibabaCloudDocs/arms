---
keyword: [ARMS, EDAS, real-time, diagnostics, screen monitoring]
---

# Real-time diagnostics

The real-time diagnostics feature is suitable for scenarios where you want to monitor application performance and identify the cause of problems within a short period of time. This topic describes how to use the real-time diagnostics feature.

If you want to monitor the performance of an application for a short period of time, such as releasing an application or performing stress tests on an application, you can use the real-time diagnostics feature. After the real-time diagnostics feature is enabled for an application, ARMS continuously monitors the application for 5 minutes and reports all the data of the traces during this period. Then, you can use the method stack waterfall chart and thread profiling to identify the causes of exceptions based on the trace that shows performance problems.

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

2.  On the Applications page, click the name of the application.

3.  In the left-side navigation pane, choose **Application Diagnosis** \> **Real-time Diagnosis**.


## Enable and disable real-time diagnostics

The first time you access the Real-time Diagnosis page, real-time diagnostics is automatically enabled. To enable real-time diagnostics in other cases, click **Enable real-time diagnosis** in the upper-right corner.

Real-time diagnostics is automatically enabled for 5 minutes and then disabled. To disable real-time diagnostics, click **Terminate Real-time Diagnosis** in the upper-right corner.

## View real-time monitoring data

In the **Real-time Requests Distribution** and **Requests by Response Time** sections, you can view the statistics of the last 1,000 requests captured as of the current point in time.

![Page Realtime Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54055.png)

In the chart of the **Real-time Requests Distribution** section, select a time range. Data of the selected time range can be set as visible. The chart shows data only within this time range. Click **Reset** in the upper-right corner of the chart and the default view can be restored.

![Expanded Time Range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54056.png)

## Filter monitoring data

You can filter request monitoring data displayed on the page by operation name or IP address.

1.  Click the **+** icon above the **Real-time Requests Distribution** section.

2.  Select an API operation or IP address from the drop-down list and click **Search**.

    Only the request monitoring data of the selected operation is displayed on the page.


## View information of traces

On the **Traces** and **Interfaces Aggregated** tabs, you can view information of all traces captured in the corresponding period. Click a trace ID to access the **Link Invocation** page. Use the local method stack waterfall chart and thread profiling to identify the causes of exceptions.

![Aggregated by API](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54058.png)

**Related topics**  


[Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md)

[Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)

