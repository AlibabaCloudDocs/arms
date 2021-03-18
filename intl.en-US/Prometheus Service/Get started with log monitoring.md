# Get started with log monitoring

You can create a log monitoring task to obtain the statistics of the specified metrics, generate the data and reports that you need, and flexibly configure alerts.

## Background information

The log monitoring feature of Application Real-Time Monitoring Service \(ARMS\) allows you to create custom monitoring tasks. The process of creating a custom monitoring task contains two key steps: configure the data source and configure metrics, as shown in the following figure.

![ARMS Custom Monitoring Job Creation](../images/p44527.png "Process of creating a log monitoring task")

## Create a log monitoring task

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Scenario-based Traces** \> **Log-Based Metric**.
3.  On the Log-Based Metric page, click **Create Log-Based Metric** in the upper-right corner.
4.  On the Create Log-Based Metric page, set the parameters in the Log source configuration section.

    |Parameter|Description|
    |---------|-----------|
    |Task name|The name of the log monitoring task.|
    |Application \(optional\)|The application to which the log monitoring task applies. After you specify an application, you can filter log monitoring tasks by application on the Log-Based Metric page.|
    |Select a log source|If no log source is available in the drop-down list, click **Synchronize LogHub**.After you select a log source, logs are automatically captured for preview. You can also click **Log preview** in the upper-right corner of the **Preview of log** section to preview the logs. |

    **Note:**

    -   Before you synchronize data from log sources, make sure that you have activated [Alibaba Cloud Log Service](https://www.aliyun.com/product/sls?spm=a2c4g.11186623.2.11.102f5facwFucs7) and you are using a RAM user that has been authorized to access Log Service or an Alibaba Cloud account.
    -   ARMS captures up to 20 records from the logs of the specified machine. A temporary pre-capturing channel must be set up. Therefore, it usually takes about 30 seconds to capture log data.
    -   If log data fails to be pre-captured, check whether the selected log source is correct.
5.  In the Metric configuration section, configure the timestamp field and metric. Then, click **Save**.

    In the Configure the metric name step, click **Add Metric**. Set the metric name, metric value field, and aggregation dimension. Click **Add Filter** and add a filter condition for the metric.

    |Parameter|Description|
    |---------|-----------|
    |Configure the timestamp field|The field that indicates the timestamp in the log data. If the log data does not have a timestamp field, you can select **Use the system timestamp** to monitor log data that is generated at the current time point.|
    |Configure the metric name|To add metrics, click **Add Metric**.|
    |Metric name|The name of the metric.|
    |value field|The measure that you want to use to monitor the application. Select a NUMERIC field from the log data. An ARMS metric provides real-time computing results returned by aggregate functions such as Count, Max, Min, Sum, and Avg. If you want to count only the number of log entries, select **count only**.|
    |GroupBy|The dimension that you want to use to monitor the application. Select a non-NUMERIC field from the log data. For example, you can specify the brand name as an aggregation dimension to count the sales of each brand. You can select up to eight aggregation dimensions.|
    |Filters|To add filter conditions, click **Add Filter**.Select a field from the log data as the key in the filter condition. For example, you can set a filter condition where the value of the log\_type parameter is engine. |

6.  Click **Alert configuration**. In the Alert configuration section, click **New Alert** and set an alert rule. In the upper-right corner of the Alert configuration section, click **Save**.

    For an alert rule, you can directly enter the expression or set the expression by following the on-screen instructions. The expression must follow the PromQL syntax.

    **Note:** When an alert is enabled and triggered, the PrometheusGroup contact group is notified.


## Manage log monitoring tasks

On the Log-Based Metric page, you can view all the created log monitoring tasks.

-   Enter the name of a log monitoring task or metric in the search box in the upper part of the page to filter log monitoring tasks.
-   Click the name of a log monitoring task to hide or show the metrics involved in the task.
-   Find the log monitoring task that you want and click **Edit** in the upper-right corner. On the Log-Based Metric Settings page, modify the task on the Rule configuration tab or delete the task on the Delete tab.

    **Note:** If you delete a log monitoring task, all data of the task is deleted and cannot be restored.

-   Find the log monitoring task that you want, click **More** in the upper-right corner, and then select an option from the shortcut menu to start or stop the task.
-   Find the log monitoring task that you want and click **Dashboard** in the upper-right corner to view the monitoring data in a dashboard.

    **Note:** The dashboard configuration is reset each time you modify the log monitoring task. After you modify the dashboard configuration, save the configuration and export the dashboard as early as possible.


