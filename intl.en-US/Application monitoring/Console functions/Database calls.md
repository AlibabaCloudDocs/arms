# Database calls

This topic shows you how to view the information about calls to the database of an application. You can obtain an overview of the database calls of the application and view the information about SQL calls, exceptions, call sources, and operation snapshots.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the left-side navigation pane, click **Database Invocation**.

6.  On the page that appears, select a database and set the time period.

    ![Database calls](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2534424161/p235852.png)

7.  After you complete the settings, perform the following operations as required:

    -   On the **Overview** tab, obtain an overview of the database calls of the application.
    -   Click the **SQL Analysis** tab to view the SQL analysis of the application.
    -   Click the **Exception Analysis** tab to view the database call exceptions of the application.
    -   Click the **Call source** tab to view the information about the applications that call the database of the application.
    -   Click the **Interface Snapshot** tab to view the snapshots of the database operations that are called in the application.

## Overview

The **Overview** tab displays the information about the database. You can view the call relationship topology, time series curve of the number of requests, time series curve of the response time, and time series curve of the number of errors.

![Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2534424161/p235853.png)

1.  On the **Overview** tab, perform the following operations as required:

    -   Click the ![Settings](../images/p232147.png) icon to configure the display settings of the application topology.

        **Note:** The settings are stored in the browser and remain effective the next time you access the Overview tab.

    -   Click the plus sign or scroll the mouse wheel up to zoom in the application topology.
    -   Click the minus sign or scroll the mouse wheel down to zoom out the application topology.
    -   Click the RESET icon to restore the application topology to the default size.
    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230759.png)Icon to view the API details for this metric.
    -   Click ![alert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3134334161/p231972.png)Icon to create an alarm for the metric. For more information, see [Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md).

## SQL analysis

The **SQL Analysis** tab displays the column chart of the number of SQL calls, the time series curves of the response time, and a list of SQL statements that are executed in the database.

![SQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236052.png)

1.  On the **SQL Analysis** tab, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230759.png)Icon to view the API details for this metric.
    -   To view the SQL call statistics of an SQL statement, click **Invocation Statistics** in the **Actions** column of the SQL statement.
    -   To view the snapshots of the operation that is called by an SQL statement, click **Interface Snapshot** in the **Actions** column of the SQL statement.

## Exception analysis

The **Exception Analysis** tab displays the information about exceptions of the database.

![Exception Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236127.png)

1.  On the **Exception Analysis** tab, perform the following operations as required:

    **Note:** To filter exceptions, perform the following steps: In the left-side navigation pane, click **Application Settings**. On the page that appears, click the **Custom Configuration** tab. In the **Advanced Settings** section, set the **Whitelist** field.

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230759.png)Icon to view the API details for this metric.
    -   To view the statistics of an exception, click **Invocation Statistics** in the **Actions** column of the exception.
    -   To view the details of an exception, click **Details** in the **Actions** column of the exception.

## Call source

The **Call source** tab displays the information about the call sources of the database.

![Call source](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236346.png)

1.  On the **Call source** tab, perform the following operations as required:

    -   To view the information about an application that calls the database or information about a database operation that is called, enter the application or operation name in the search box and click the ![Search](../images/p236349.png) icon.
    -   To view the snapshots of a database operation that is called by a call source, click **view details** next to the operation.
    -   Move the cursor over the statistics chart to view the statistics.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.

## Operation snapshot

The **Interface Snapshot** tab displays the snapshots of all operations that are called in the database.

![Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236484.png)

1.  On the **Interface Snapshot** tab, perform the following operations as required:

    -   To view the snapshots of an operation, enter the operation name in the search box and click the ![Search](../images/p236472.png) icon.
    -   To view a trace of an operation, click the trace ID in the **TraceId** column of the operation.
    -   To view the logs of an operation, click **View Logs** in the **Actions column** of the operation.

