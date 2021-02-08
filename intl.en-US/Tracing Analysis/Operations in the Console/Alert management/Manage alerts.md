# Manage alerts

In the Alert History module of the Tracing Analysis console, you can manage all the alert rules within your Alibaba Cloud account and query the alert event history and alert notification history.

## Manage alert rules

The alert rules that you created are displayed on the Alarm Policies page. You can start, stop, edit, and delete the alert rules. You can also view alert details.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alert History** \> **Alert Rules and History**.

3.  On the **Alert Rules** tab, enter an alert name in the search bar and click **Search**.

    **Note:** You can enter part of an alert name in the search bar to perform a fuzzy search.

4.  In the **Actions** column of the search result table, click buttons to manage an alert rule as needed.

    ![Page Alerts](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928043290_zh-CN.png)

    -   To edit an alert rule, click **Edit**. In the Edit Alarm dialog box, edit the alert rule and click **Save**.
    -   To delete an alert rule, click **Delete**. In the Delete message, click **Delete**.
    -   To start a stopped alert rule, click **Start**. In the OK message, click **Start**.
    -   To stop a running alert rule, click **Stop**. In the Stop message, click **OK**.
    -   To view the alert event history and alert notification history, click **View Alert Detail**. On the **Alert History** tab, view related records.

## Query the alert history

On the **Alert History** tab, you can view historical records about when and why an alert rule was triggered, and about alert notifications that are sent to specified alert contacts.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alert History** \> **Alert Rules and History**.

3.  On the Alarm Policies page, click the **Alert History** tab.

4.  On the **Alert History** tab, set the **Trigger State** and **Alarm Name** parameters and click **Search**.

    The line charts and column charts on the tab show the relationships between alert data and alert trigger events, and the alert trigger details. The line charts represent the alert data and the column charts represent the alert events.

    ![Tab Alert History](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928143291_zh-CN.png)

5.  Scroll down to the lower part of the page and view the history of alert events on the Alert Event History tab.

    **Note:** Alert notifications are sent only when the alert rule is in the **Triggered** state. In this state, a red dot is displayed in the **Trigger** column.

    ![Tab Alert Event History](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152335/156136928143292_zh-CN.png)

6.  Click the Alarm Post History tab to view the history of alert notifications that are sent for triggered alerts. The alert notifications include text messages and emails.


**Related topics**  


[Create an alert contact](/intl.en-US/Operations in the Console/Alert management/Create an alert contact.md)

