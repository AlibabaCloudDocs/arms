# Manage alerts

You can manage all alert rules under your account and query alert events and alert notification records through the alert management module in the tracing analysis console.

## Manage an alert rule

The created alarm rule is displayed on the alarm rules and history page. You can start, stop, edit, and delete the alert rules. You can also view alert details.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alarm management** \> **Alarm rules**.

3.  On the **alarm rules and history** tab page, enter an alarm name in the search box and then click **search**.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

4.  In the search results list of **operation** column, on-demand target alarm rule to take the following actions:

    ![Page Alerts](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928043290_zh-CN.png)

    -   To edit an alarm rule, click **edit**. In the edit alarm dialog box, edit the alarm rule and click **save**.
    -   To delete an alarm rule, click **delete**. In the delete dialog box, click **delete**.
    -   To start a stopped alert rule, click **start**. In the start dialog box, click **OK**.
    -   To stop the started alarm rule, click **stop**. In the stop dialog box, click **OK**.
    -   To view the alert event history and alert notification history, click **view alert details** and view the **alert history** records on the alert history query tab.

## Query the alert history

You can **click alarm history** to search for historical records about when an alarm rule is triggered and the alarm notifications sent to specific alarm contacts after the rule is triggered.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alarm management** \> **Alarm rules**.

3.  On the alarm rules and history page, click the **alarm history** tab.

4.  On the **alarm history** tab, select or enter the alarm **type**, **event trigger status**, and **alarm name**. Then click **search**.

    The line charts and bar charts on the tab show the relationship between alert data and alert trigger events, also the alert trigger details. The line chart represents the alert data and the bar chart represents the alert events.

    ![Tab Alert History](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928143291_zh-CN.png)

5.  Click the alarm event history tab at the bottom to view the history of alarm events.

    **Note:** An alarm notification is sent only when the **triggering status** is **triggered** \(red dot in the triggering status column\).

    ![Tab Alert Event History](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928143292_zh-CN.png)

6.  Click the alarm sending History tab to view the records of alarm notifications \(by SMS, email, or other means\) that have triggered alarms.


**Related topics**  


[Create an alert contact](/intl.en-US/Console guide/Alerting/Create an alert contact.md)

