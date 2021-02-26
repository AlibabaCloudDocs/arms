# SQL analysis

This topic shows you how to view the SQL analysis of an application.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select an instance where the application is deployed, set the time period, and then click the **SQL Analysis** tab.

    ![SQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6625424161/p230688.png)


## SQL call statistics

The **SQL Calls** section displays the time series curve that indicates the SQL call statistics of the application in the specified time period.

![SQL Calls](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7625424161/p232883.png)

1.  In the **SQL Calls** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230759.png)Icon to view the API details for this metric.

## SQL statement list

The SQL statement list displays all SQL statements that are executed in the application in the specified time period.

![SQL statement list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7625424161/p235824.png)

1.  In the SQL statement list, perform the following operations as required:

    -   To view the time series curve of the SQL call statistics of an SQL statement, click **Invocation Statistics** in the **Actions** column of the SQL statement.
    -   To view the snapshots of the operation that is called by an SQL statement, click **Interface Snapshot** in the **Actions** column of the SQL statement.

        For more information, see [Operation snapshot](/intl.en-US/Application monitoring/Console functions/Application details/Operation snapshots.md).


