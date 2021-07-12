# Log analysis

When the Deployment has a business exception, you can analyze the business logs to accurately locate the business exceptions.

-   The application is monitored by Application Real-Time Monitoring Service \(ARMS\). For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).
-   Log Service is activated. Log on to the [Log Service console](https://sls.console.aliyun.com), activate Log Service as prompted.
-   A Log Service project is created. For more information, see [Create a project](/intl.en-US/Preparation/Manage a project.md).
-   A Logstore is created. For more information, see [Create a Logstore](/intl.en-US/Preparation/Manage a Logstore.md).

## Step 1: Associate business logs with trace IDs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application that you want to manage.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.

4.  Log on to the Custom configurationtab **Business log association settings**area, turn on **Associate business logs with TraceId**and then bind the project and Logstore.

    ![Link Business Logs with TraceId](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7527900161/p164105.png)

5.  Log on to the Custom configurationClick in the lower-left corner of the tab. **Save**.


## Step 2: Query and analyze business logs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Container Monitoring**.

3.  In the top navigation bar, select the region where your instance is located.

4.  Log on to the **Container monitoring**On the page that appears, click the name of the Kubernetes cluster.

5.  In the left-side navigation pane, choose **Log analysis**.

6.  On the Log Analysis page, perform the following operations:

    1.  Enter a query statement in the search box.

        A query analysis statement consists of a query statement and an analysis statement in the following format Query statement \| Analysis statement. For more information about the syntax of the query and analysis statement, see [Search syntax](/intl.en-US/Index and query/Query/Search syntax.md), [SQL analysis syntax](/intl.en-US/Index and query/Analysis grammar/General aggregate functions.md).

    2.  Specify the time range for the query and analysis.

        You can select a relative time, set a time frame, or customize a time range.

        **Note:** The query results may contain logs that are generated 1 minute earlier or later than the specified time range.

    3.  Click **Query /Analysis**to view the query and analysis results.

    ![Log Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6754397161/p254446.png)


