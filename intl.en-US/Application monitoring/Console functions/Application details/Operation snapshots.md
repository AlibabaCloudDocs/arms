# Operation snapshots

This topic shows you how to view the snapshots of all operations that are called in an application. You can view the time when snapshots are created, the time that is consumed for calling each operation, and the status of each operation.

The Application Real-Time Monitoring Service \(ARMS\) agent is installed for an application. For more information, see [Overview](/intl.en-US/Application monitoring/Quick start/Overview.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  Log on to the **Left-side navigation pane**Place place your cursor over the vertical dots next to **Application details**.

6.  On the **Application Details** page, select an instance where the application is deployed, set the time period, and then click the **Interface Snapshot** tab.

    ![Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6075424161/p235769.png)


## Operation snapshot

The **Interface Snapshot** tab lists all operations that are called in the application in the specified time period.

![Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6075424161/p235775.png)

1.  On the **Interface Snapshot** tab, perform the following operations as required:

    -   To view the snapshots of an operation, enter the operation name in the search box and click the ![Search](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5262684161/p235841.png) icon.
    -   To view a trace of an operation, click the trace ID in the **TraceId** column of the operation.
    -   To view the logs of an operation, click **View Logs** in the **Actions** column of the operation.

