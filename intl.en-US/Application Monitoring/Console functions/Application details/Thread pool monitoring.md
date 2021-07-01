# Thread pool monitoring

You can use the thread pool monitoring feature to view metrics of the thread pool of an application that is monitored by Application Real-Time Monitoring Service \(ARMS\). The provided metrics include the number of core threads, number of existing threads, maximum number of threads allowed, number of active threads, number of submitted tasks, and maximum number of tasks allowed in the task queue.

Your application is monitored by ARMS. For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).

## Enable thread pool monitoring

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  In the top navigation bar, select the region where your application is deployed.

4.  On the **Applications** page, click the name of your application.

5.  In the left-side navigation pane, click **Application Settings**.

6.  Click the **Custom Configuration** tab. On the Custom Configuration tab, turn on **Thread pool monitoring** in the **Advanced Settings** section.

    **Note:** The thread pool monitoring feature can monitor the thread pools in frameworks such as Apache Tomcat, Apache Dubbo, and High-speed Service Framework \(HSF\) and allows you to view metrics of the thread pools. To enable the feature, you must update the ARMS agent to the latest version. For more information, see [Update the ARMS agent for Java applications](/intl.en-US/Application Monitoring/Update the ARMS agent for Java applications.md). The feature takes effect after you restart your application.


## View metrics for thread pool monitoring

After you enable the thread pool monitoring feature, you can view the metrics on the **Thread pool monitoring** tab of the **Application Details** page. On the **Thread pool monitoring** tab, you can view different time series curves that show the following metrics of the thread pool of your application: the number of core threads, number of existing threads, maximum number of threads allowed, number of active threads, number of submitted tasks, and maximum number of tasks allowed in the task queue.

|Metric|Description|
|------|-----------|
|Core Size|The number of core threads in the thread pool.|
|Current Size|The number of threads that exist in the thread pool.|
|Max Size|The maximum number of threads allowed in the thread pool.|
|Active Count|The number of active threads that are processing tasks.|
|Executed Task Count|The number of tasks that are submitted to the thread pool.|
|Queue Size|The maximum number of tasks allowed in the task queue.|

**Note:** A thread is created to process a newly submitted task in the following scenarios: \(1\) The number of existing threads in a thread pool is less than that of core threads. In this case, a thread is created even if idle threads exist. \(2\) The number of existing threads in a thread pool is greater than that of core threads. The number of tasks in the task queue reaches the upper limit. The number of existing threads in a thread pool cannot exceed the maximum number of threads allowed in the thread pool.

On the **Thread pool monitoring** tab, you can perform the following operations:

-   Move the pointer over a chart and view the detailed statistics.
-   Click the name of a metric such as Core Size on a chart to show or hide the metric.

    **Note:** Each chart must contain at least one visible metric. Therefore, if only one metric is displayed in a chart, you cannot hide this metric.


