# Quickly create ARMS alerts

By creating alerts for monitoring jobs, you can actively detect exceptions. This topic describes how to create application monitoring alerts, browser monitoring alerts, and custom monitoring alerts by using an instance.

Make sure that you have created a monitoring job and an administrative contact group.

## Create an application monitoring alert

To create an alert on Java Virtual Machine-Garbage Collections \(JVM-GCs\) in interval-valued comparison for an application monitoring job, perform the following steps:

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home). In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.
2.  On the Alert Policies page, choose **Create Alarm** \> **Application Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alarm Name, for example, alert on JVM-GCs in interval-valued comparison.
    2.  In the **Application Site** field, select the monitoring job you created.
    3.  In the **Type** field, select the type of the monitoring metric, for example, JVM\_Monitoring.
    4.  Set Dimension to Traverse.
    5.  Set Alarm Rules.
        1.  Select **Meet All of the Following Criteria**.
        2.  Edit an alert rule. For example, an alert is triggered when the value of N is 5 and the average value of JVM\_FullGC increases by 100% compared with that in the previous hour.

            **Note:** To add another alert rule, click **+** on the right of **Alarm Rules**.

    6.  Set Notification Mode. For example, select Email.
    7.  Set Notification Receiver. In the **Contact Groups** box, click the name of a contact group. If the contact group appears in the **Selected Groups** box, the setting is successful.

## Create a browser monitoring alert

To create a page metric alert on the JavaScript error rate and JavaScript error count, perform the following steps:

1.  Log on to the ARMS console. In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alert Policies page, choose **Create Alarm** \> **Browser Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alarm Name, for example, page metric alert.
    2.  In the **Application Site** field, select the monitoring job you created.
    3.  In the **Type** field, select the type of the monitoring metric, for example, Page\_Metric.
    4.  Set Dimension to Traverse.
    5.  Set Alarm Rules.
        1.  Select **Meet All of the Following Criteria**.
        2.  Edit an alert rule. For example, an alert is triggered when the value of N is 10 and the average value of JavaScript error rate is at least 20.
        3.  To add another alert rule, click **+** on the right of Alarm Rules. For example, an alert is triggered when the value of N is 10 and the JavaScript error count is at least 20.
    6.  Set Notification Mode. For example, select SMS and Email.
    7.  Set Notification Receiver. In the **Contact Groups** box, click the name of a contact group. If the contact group appears in the **Selected Groups** box, the setting succeeds.

## Create a custom monitoring alert

To create a user access alert for a custom monitoring job, perform the following steps:

1.  Log on to the ARMS console. In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alert Policies page, choose **Create Alarm** \> **Custom Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

1.  Enter Alarm Name, for example, user access notification.
2.  Set Type to **Create Alarm Based On Existing Drilled-down Dataset**.
3.  Set Alarm Variable Definition. Select a dataset for the a variable and set Drill-down Dimension to Traverse.

    **Note:** To define another alert variable, click **+** on the right of **Alarm Variable Definition**. In the text box that appears, define the b variable.

4.  Set Alarm Rules.
    1.  Select **Meet All of the Following Criteria**.
    2.  Edit an alert rule. For example, an alert is triggered when the value of N is 1 and the average number of ARMS agents that you created is at least 0.

        **Note:** You can also include a simple composite metric in the alert rule. For example, an alert is triggered when the value of N is 1 and the average value of dataset A/dataset B is at least 5.

5.  Set Notification Mode. For example, select Email.
6.  Set Notification Receiver. In the **Contact Groups** box, click the name of a contact group. If the contact group appears in the **Selected Groups** box, the setting succeeds.

