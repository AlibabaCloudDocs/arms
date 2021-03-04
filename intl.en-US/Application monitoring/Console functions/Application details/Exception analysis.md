# Exception analysis

This topic shows you how to view the exception analysis of an application.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select an instance where the application is deployed, set the time period, and then click the **Exception Analysis** tab.

    ![Exception Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0352684161/p232939.png)


## Exception statistics

The **Exceptions** section displays the stacked column chart of the exception statistics of the application in the specified time period and the exception list.

![Exception statistics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8841334161/p235678.png)

1.  In the **Exceptions** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.
    -   Click ![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230753.png)Icon to view the statistics of the metric in a certain time period or compare the statistics of the same time period on different dates.
    -   Click ![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9624334161/p230759.png)Icon to view the API details for this metric.

## Exception list

The exception list displays all exceptions of the application in the specified time period.

1.  In the exception list, perform the following operations as required:

    ![Exception list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8841334161/p235828.png)

    **Note:** To filter exceptions, perform the following steps: In the left-side navigation pane, click **Application Settings**. On the page that appears, click the **Custom Configuration** tab. In the **Advanced Settings** section, set the **Whitelist** field.

    -   To view the stacked column chart of an exception, click **Invocation Statistics** in the **Actions** column of the exception.
    -   To view the snapshots of the operations that are called when an exception occurs, click **Interface Snapshot** in the **Actions** column of the exception.

        For more information, see [Operation snapshot](/intl.en-US/Application monitoring/Console functions/Application details/Operation snapshots.md).

    -   To view the details of an exception, click **Details** in the **Actions** column of the exception.

