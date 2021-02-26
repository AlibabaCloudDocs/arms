# Error analysis

This topic shows you how to view the error analysis of an application.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select an instance where the application is deployed, set the time period, and then click the **Error Analysis** tab.

    ![Error Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8575424161/p231802.png)


## Number of errors

The **Errors** section displays the time series curve that indicates the number of errors of the application in the specified time period.

![Errors](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8575424161/p235714.png)

1.  In the **Errors** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](../images/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](../images/p230759.png)Icon to view the API details for this metric.

## HTTP status code

The **HTTP - Status Code** section displays the time series curve that indicates the HTTP status code statistics of the application in the specified time period.

![HTTP - Status Code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8575424161/p235727.png)

1.  In the **HTTP - Status Code** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click legend to hide or show the data.
    -   Click ![chart](../images/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](../images/p230759.png)Icon to view the API details for this metric.

## Error list

The error list displays all errors of the application in the specified time period.

![Error list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8575424161/p235738.png)

1.  In the error list, perform the following operations as required:

    -   To view a trace of an error, click the trace ID in the **TraceId** column of the error.
    -   To view the logs of an error, click **View Logs** in the **Actions** column of the error.

