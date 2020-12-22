# Manage alerts

On the Alert Policies page, you can manage all the alert rules within your Alibaba Cloud account and query the history of alert events and alert notifications.

## Manage alert rules

On the Alert Policies page, the alert rules that you created in Application Monitoring, Browser Monitoring, and Custom Monitoring are displayed. You can start, stop, edit, and delete the alert rules. You can also view alert details. For more information about how to create alert rules, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

3.  On the **Alert Policies** page, enter the alert name in the search box and click **Search**.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

4.  You can perform the following operations on an alert rule in the **Actions** column based on your business requirements:

    -   To edit an alert rule, click **Edit** in the Actions column. In the Edit Alarm dialog box, edit the alert rule and click **Save**.
    -   To delete an alert rule, click **Delete** in the Actions column. In the Delete dialog box, click **Delete**.
    -   To start a stopped alert rule, click **Start** in the Actions column. In the OK dialog box, click **Start**.
    -   To stop a running alert rule, click **Stop** in the Actions column. In the Stop dialog box, click **OK**.
    -   To view the alert event history and alert sending history, click the **Alert History** tab. You can then click the **Alert Event History** and **Alarm Post History** tabs to view the history.

## Query the alert history

On the **Alert History** tab, you can view historical records that indicate when and why an alert rule was triggered. You can also view historical records about the alert notifications sent to specified alert contacts.

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**. On the Alert Policies page, click the Alert History tab.

2.  On the **Alert History** tab, select or enter **Type**, **Trigger State**, and **Alert Name**, and then click **Search**.

3.  On the Alert Policies page, you can view historical records of alert events.

    **Note:** Alert notifications are sent only if the alert rule is in the **Triggered** state. In this state, a red dot is displayed in the **Trigger** column.

4.  Click the Alarm Post History tab to view the history of alert notifications that were sent for triggered alerts. The alert notifications include SMS messages and emails.


**Related topics**  


[Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

[Create a contact](/intl.en-US/Dashboard and alerting/Create contacts.md)

[t1918101.md\#]()

