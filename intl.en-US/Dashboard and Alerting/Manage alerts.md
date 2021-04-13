# Manage alerts

On the Alarm Policies page, you can manage all the alert rules within your Alibaba Cloud account and query the history of alert events and alert notifications.

## Manage alert rules

On the Alarm Policies page, the alert rules that you created in Application Monitoring, Browser Monitoring, and Custom Monitoring are displayed. You can perform operations on the alert rules. For example, you can start, stop, edit, delete alert rules, and view alert details. For more information about how to create alert rules, see [Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md).

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

3.  On the **Alarm Policies** page, enter the alert name in the search box and click **Search**.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

4.  You can perform the following operations on an alert rule in the **Actions** column based on your business requirements:

    -   To edit an alert rule, click **Edit** in the Actions column. In the Edit Alarm dialog box, edit the alert rule and click **Save**.
    -   To delete an alert rule, click **Delete** in the Actions column. In the Delete message, click **Delete**.
    -   To start a stopped alert rule, click **Start** in the Actions column. In the OK message, click **Start**.
    -   To stop a running alert rule, click **Stop** in the Actions column. In the Stop message, click **OK**.
    -   To view the alert event history and alert sending history, click **View Alert Detail** in the Actions column. You can then click the **Alert Event History** and **Alarm Post History** tabs to view the history.
    ![Alarm History](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7913978061/p43290.png)


## Query alert history

On the **Alert History** tab, you can view historical records that indicate when and why an alert rule was triggered. You can also view historical records about the alert notifications sent to specified alert contacts.

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**. On the Alert Policies page, click the Alert History tab.

2.  On the **Alert History** tab, select or enter **Type**, **Trigger State**, and **Alarm Name**, and then click **Search**.

3.  On the Alarm Policies page, view historical records of alert events.

    **Note:** Alert notifications are sent only when an alert rule is in the **Triggered** state. In this state, a red dot is displayed in the **Trigger** column.

4.  Click the Alarm Post History tab to view the history of alert notifications that were sent for triggered alerts. The alert notifications include text messages and emails.


**Related topics**  


[Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md)

[Create a contact](/intl.en-US/Dashboard and Alerting/Create contacts.md)

[Create a contact group](/intl.en-US/Dashboard and Alerting/Create a contact group.md)

