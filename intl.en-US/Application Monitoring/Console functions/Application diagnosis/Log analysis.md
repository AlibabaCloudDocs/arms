# Log analysis

The log analysis feature enables you to accurately identify business exceptions for your application based on business logs.

-   The application is monitored by Application Real-Time Monitoring Service \(ARMS\). For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).
-   Log Service is activated. If Log Service is not activated, log on to the [Log Service console](https://sls.console.aliyun.com) and activate Log Service by following the on-screen instructions.
-   A Log Service project is created. For more information, see [Create a project](/intl.en-US/Data Collection/Preparation/Manage a project.md).
-   A Log Service Logstore is created. For more information, see [Create a Logstore](/intl.en-US/Data Collection/Preparation/Manage a Logstore.md).

## Step 1: Associate business logs with trace IDs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.

4.  On the Custom Configuration tab, turn on **Link Business Logs with TraceId** in the **Business Log Linking Settings** section. Then, specify the project and Logstore that store the business logs to be associated with trace IDs.

    ![Link Business Logs with TraceId](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164105.png)

5.  On the Custom Configuration tab, click **Save** in the lower-left corner.


## Step 2: Query and analyze business logs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, choose **Application Diagnosis** \> **Log Analysis**.

4.  On the Log Analysis page, perform the following operations:

    1.  Enter a query statement in the search box.

        A query statement consists of a search statement and an analytic statement in the format of Search statement\|Analytic statement. For more information, see [Search syntax](/intl.en-US/Index and query/Query/Search syntax.md) and [SQL syntax and functions](/intl.en-US/Index and query/Analysis grammar/General aggregate functions.md).

    2.  Specify the time range for the query and analysis.

        You can select a relative time, set a time frame, or customize a time range.

        **Note:** The query results may contain logs that are generated 1 minute earlier or later than the specified time range.

    3.  Click **Search & Analyze** to view the query and analysis results.

    ![Log Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6754397161/p254446.png)


