# NoSQL analysis

This topic shows you how to view the NoSQL analysis of an application.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select an instance where the application is deployed, set the time period, and then click the **NoSQL Analysis** tab.

    ![NoSQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1725424161/p236398.png)


## NoSQL call statistics

The **SQL Calls** section displays the time series curve that indicates the NoSQL call statistics of the application in the specified time period.

![SQL Calls](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1725424161/p236412.png)

1.  In the **SQL Calls** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](../images/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](../images/p230759.png)Icon to view the API details for this metric.

## Operation command list

The operation command list displays all operation commands that are run in NoSQL calls of the application in the specified time period.

![Operation command list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1725424161/p236413.png)

1.  In the operation command list, perform the following operations as required:

    -   To view the NoSQL call statistics of an operation command, click **Invocation Statistics** in the **Actions** column of the operation command.
    -   To view the snapshots of the operation that is called by an operation command, click **Interface Snapshot** in the **Actions** column of the operation command.

        For more information, see [Operation snapshot]().


