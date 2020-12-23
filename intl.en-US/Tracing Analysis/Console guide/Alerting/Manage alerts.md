# Manage alerts

On the alert Policies page, you can manage all the alert rules under your account and query the history of alert events and alert posts.

## Manage alert rules

The alert rules that you create in Application Monitoring, Browser Monitoring, and Custom Monitoring all appear on the Alert Policies page. You can take actions to the alert rules, including start, stop, edit, delete alert rules, and view alert details. For more information about how to create alert rules, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose**Alerts** \> **Alert Policies**.

3.  On the **Alert Rules** tab, enter the alert name in the search box, then click **Search**.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

4.  In the **Actions** column, you may take actions on the filtered alert rules, as needed:

    -   To edit an alert rule, click **Edit**. In the Edit Alert dialog box, edit the alert rule, and click **Save**.
    -   To delete an alert rule, click **Delete**. In the Delete dialog box, click **Delete**.
    -   To start a stopped alert rule, click **Start**, and in OK dialog box, click **Start**.
    -   To stop a running alert rule, click **Stop**, and then click **OK** in the Stop dialog box.
    -   To view the alert event history and alert post history, click **View Alert Detail**, and view related records on the **Alert Event History** tab.

## Query alert history

You can view historical records about when and why an alert rule was triggered, and about the alert notification records sent to specified alert contacts on the **Alert History** tab.

1.  On the Alert Policies page, click the **Alert History** tab.

2.  On the **Alert History** tab, select or enter the **Alert Type**, **Trigger State** and **Alert Name**, and then click **Search**.

    The line charts and bar charts on the tab show the relationship between alert data and alert trigger events, also the alert trigger details. The line chart represents the alert data and the bar chart represents the alert events.

3.  Scroll down to the bottom, view the history of alert events on the Alert Event History tab.

    **Note:** Alert notifications are sent only when the trigger state is **triggered**. \(**Trigger** column contains a red dot.\)

4.  Click the Alert Post History tab to view the records of alert notifications \(such as SMS and email\) that were sent for triggered alerts.


[Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

[Create contacts](/intl.en-US/Dashboard and alerting/Create contacts.md)

[Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md)

