# Identify business exceptions by analyzing traces and logs

The difficulty and low efficiency in identifying business exceptions have always been performance bottlenecks of the application monitoring feature of Application Real-Time Monitoring Service \(ARMS\). However, you can use the application monitoring feature of ARMS together with traces and logs to efficiently and accurately identify business exceptions. This improves the efficiency of development and diagnostics in a microservices framework.

-   Log Service is activated. Log on to the [Log Service console](https://sls.console.aliyun.com) and activate Log Service by following the on-screen instructions.
-   A project is created. For more information, see [Create a project](/intl.en-US/Data Collection/Preparation/Manage a project.md).
-   A Logstore is created. For more information, see [Create a Logstore](/intl.en-US/Data Collection/Preparation/Manage a Logstore.md).

Before you identify business exceptions by analyzing traces and logs, you must understand the following terms: metric, tracing, and logging.

-   Metric: The key metrics of an application include Application Service Request, Application Service Average Response Time, and Application Dependent Service Request.
-   Tracing: All activities of an application, such as API calls and responses, are recorded in traces.
-   Logging: All activities of an application, such as API calls and responses, are recorded in business logs.

When a business exception occurs, the statistical chart for an application metric shows obvious fluctuations. You can roughly analyze the business exception based on the chart. You can also analyze the complete traces and business logs to accurately identify the business exception.



## Associate business logs with trace IDs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.

4.  On the Custom Configuration tab, turn on **Link Business Logs with TraceId** in the **Business Log Linking Settings** section. Then, specify the project and Logstore that store the business logs to be associated with trace IDs.

    ![Link Business Logs with TraceId](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164105.png)

5.  On the Custom Configuration tab, click **Save** in the lower-left corner.


## Troubleshoot business exceptions from the perspective of application metrics

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Application Overview**. On the page that appears, click the **Overview** tab in the upper part and select or set a time range to query in the upper-right corner.

    The **Overview** tab displays key metrics of the application, including **Application Service Request**, **Application Service Average Response Time**, and **Application Dependent Service Request**.

4.  On the **Overview** tab, drag-select a time range on the chart for an application metric.

    In this example, the **Application Service Average Response Time** metric is used.

    ![Application Service Average Response Time ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164127.png)

5.  View the traces that were generated in the time range selected in Step 4.

    1.  Click **View CallChain selected time**.

    2.  In the panel that appears, find the trace record whose status is and click the trace ID in the **TraceId** column.

        You can also click **View Logs** in the **Actions** column for the trace record to view the business logs that were generated at the specified time point. Then, you can analyze the cause of the business exception.

        ![EXception-Traceid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164417.png)

    3.  Click the **Traces** tab. In the **Method Stack** column, click the icon.

    4.  On the trace details page, find the error message. You can move the pointer over the error message to view the exception cause.

        ![Exception](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164235.png)

6.  View the business logs that were generated in the time range selected in Step 4.

    1.  Click **View Log selected time**.

    2.  On the log analysis page, find the error message of the business exception and identify the cause of the business exception.

        ![Log Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164405.png)


## Troubleshoot business exceptions from the perspective of API calls

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Interface Invocation**.

4.  On the page that appears, click the API operation that you want in the API operation list and click the **Interface Snapshot** tab on the right.

5.  On the **Interface Snapshot** tab, find the API call record whose status is .

    ![Interface Snapshot-Exception](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164414.png)

6.  View the trace for the API call.

    1.  Click the trace ID in the **TraceId** column for the API call record.

    2.  Click the **Traces** tab. In the **Method Stack** column, click the icon.

    3.  On the trace details page, find the error message. You can move the pointer over the error message to view the exception cause.

        ![Exception](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164235.png)

7.  View the logs for the API call.

    1.  Click **View Logs** in the **Actions** column for the API call record.

    2.  On the log analysis page, find the error message of the business exception and identify the cause of the business exception.

        ![Log Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164405.png)


