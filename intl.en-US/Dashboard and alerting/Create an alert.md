# Create an alert

By creating alerts, you can set alert rules for specific monitored objects. When a rule is triggered, the system sends an alert notification to the specified contact group in the specified alerting mode. This reminds you to take necessary actions to solve the problem.

-   A monitoring job is created. For more information, see [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md) and [Create a custom monitoring job]().
-   Contacts are created. Only contact groups can be set for the notification receiver of an alert.

Default behaviors of alert notifications:

-   To prevent you from receiving a large number of alert notifications in a short period of time, the system sends only one message for repeated alerts within 24 hours.
-   If no repeated alerts are generated within 5 minutes, the system sends a recovery email to notify you that the alert has been cleared.
-   After a recovery email is sent, the alert status is reset. If this alert arises again, it is deemed as a new one.

An alert widget is essentially a data display method for datasets. When you create an alert widget, a dataset is created to store the underlying data of the alert widget.

**Note:** New alerts take effect within 10 minutes. The alert check may have a delay of 1 to 3 minutes.

## Create an application monitoring alert

To create an alert for an application monitoring job on Java Virtual Machine-Garbage Collection \(JVM-GC\) times in corresponding-period comparison, perform the following operations:

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alert Policies page, choose **Create Alarm** \> **Application Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Set **Alarm Name**. Example: alert on JVM-GC times in corresponding-period comparison.

    2.  Select an application for **Application Site** and an application group for **Application Group**.

    3.  Select the type of the monitoring metrics from the **Type** drop-down list. Example: **JVM\_Monitoring**.

    4.  Set Dimension to **Traverse**.

    5.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of JVM\_FullGC increases by 100% compared with that in the previous hour.

            **Note:** To add another alert rule, click the **+** icon on the right side of **Alarm Rules**.

    6.  Set Notification Mode. For example, select Email.

    7.  Set Notification Receiver. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

    ![Application Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3608828061/p174561.png)


## Create a browser monitoring alert

To create a page metric alert on the JS error rate and JS error count, perform the following operations:

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alert Policies page, choose **Create Alarm** \> **Browser Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alert Name such as page metric alert.

    2.  In the **Application Site** field, select the monitoring job you created.

    3.  Select the type of the monitoring metric from the **Type** drop-down list. Example: **Page\_Metric**.

    4.  Set Dimension to **Traverse**.

    5.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 10 and the average value of JS error rate is at least 20.
        3.  To add another alert rule, click the **+** icon on the right side of Alarm Rules. For example, an alert is triggered when the value of N is 10 and the JS error count is at least 20.
    6.  Set Notification Mode. For example, select SMS and Email.

    7.  Set Notification Receiver. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

    ![Browser Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1667828061/p43505.png)


## Create a custom monitoring alert

To create a user access alert for a custom monitoring job, perform the following operations:

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alert Policies page, choose **Create Alarm** \> **Custom Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alarm Name such as user access notification.

    2.  Set Type to **Create Alert Based On Existing Drilled-down Dataset**.

    3.  Set Alarm Variable Definition. Select a dataset for variable a and set Drill-down Dimension to Traverse.

        **Note:**

        -   To define another alert variable, click **+** on the right side of **Alarm Variable Definition**. In the dialog box that appears, define variable b.
        -   For more information about how to create a dataset, see [t152304.md\#]().
    4.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 3 and the average number of agents that you created is at least 0.

            **Note:** You can also include a simple composite metric in the alert rule. For example, an alert is triggered when the value of N is 3 and the average value of dataset A divided by dataset B is at least 5.

    5.  Set Notification Mode. For example, select Email.

    6.  Set Notification Receiver. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

    ![Custom Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1667828061/p43507.png)


## Create a Prometheus monitoring alert

To create an alert for a Prometheus monitoring job such as an alert on network receiving pressure, perform the following operations:

1.  You can select one of the two available methods to go to the Create Alarm page.

    -   On the New DashBoard page of the [Prometheus Grafana dashboard](http://grafana.console.aliyun.com/), click theicon to go to the ARMS Prometheus Create Alarm dialog box.
    -   In the left-side navigation pane of the console, choose **Alerts** \> **Alert Policies**. On the Alert Policies page, choose **Create Alarm** \> **Prometheus** in the upper-right corner.
2.  In the **Create Alarm** dialog box, enter all required information and click **Save**.

    1.  Enter Alarm Name such as network receiving pressure alert.

    2.  Select the corresponding **cluster** of the Prometheus monitoring job.

    3.  Set **Type** to **grafana**.

    4.  Select the specific **dashboard** and **chart** to monitor.

    5.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of network receiving bytes \(MB\) is at least 3.

            **Note:** A Grafana chart may contain data of Curve A, Curve B, and Curve C. You can select one of them to monitor.

        3.  In the **PromQL** field, edit the existing PromQL statement or enter a new PromQL statement.

            **Note:** An error may be reported if a PromQL statement contains a dollar sign \($\). You must delete the equal sign \(=\) and the parameters on both sides of the dollar sign \($\) from the statement that contains the dollar sign \($\). For example, modify `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`

    6.  Set Notification Mode. For example, select SMS.

    7.  Set Notification Receiver. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

    ![Prometheus Monitoring Alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3608828061/p61774.png)


## Description of basic fields

The following table describes the basic fields of the **Create Alarm** dialog box.

![Create Alarm dialog box](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6128828061/p174562.png)

|Field|Description|Remarks|
|-----|-----------|-------|
|Application Site|The monitoring job that has been created.|Select a value from the drop-down list.|
|Type|The type of the metric.|The types for the three alerts are different:-   Application monitoring alert: This displays application entry calls, the statistics for application call types, database metrics, JVM monitoring, host monitoring, and abnormal interface calls.
-   Browser monitoring alert: This shows page metrics, interface metrics, custom metrics, and page interface metrics.
-   Custom monitoring alert: This creates alerts based on existing drilled-down datasets and existing general datasets. |
|Dimension|The dimensions for alert metrics \(datasets\). You can select None, "=", or Traverse.|-   When Dimension is set to None, the alert content shows the sum of all values of this dimension.
-   When Dimension is set to "=", you must enter the specific content.
-   When Dimension is set to Traverse, the alert content shows the dimension content that actually triggers the alert. |
|Last N Minutes|The system checks whether the data results in the last N minutes meet the trigger condition.|Valid values of N: 1 to 60.|
|Notification Mode|Email, SMS, ,Ding Ding Robot, and Webhook are supported.|You can select multiple modes. For more information about how to configure DingTalk robot, see .[Enable DingTalk chatbot alert](https://www.alibabacloud.com/help/zh/doc-detail/106247.htm)|
|Alert Quiet Period|You can enable or disable Alert Quiet Period. By default, Alert Quiet Period is enabled.|-   When Alert Quiet Period is enabled: if data remains in the triggered state, the second alert notification is sent 24 hours after the first alert is triggered. When data is recovered, you receive a data recovery notification and the alert is cleared. If the data triggers the alert one more time, the alert notification is sent again.
-   When Alert Quiet Period is disabled: if the alert is continually triggered, the system sends the alert notification every minute. |
|Alert Severity|Valid values include Warn, Error, and Fatal.|-|
|Notification Time|The time when the alert was sent. No alert notification is sent out of this time period, but alert events are recorded.|For more information about alert event history, see [Manage alerts](https://www.alibabacloud.com/help/zh/doc-detail/42966.htm).|
|Notification Content|The custom content of the alert.|You can edit the default template. In the template, the four variables, $AlertName, $AlertFilter, $AlertTime, and $AlertContent, are preset. \(Other preset variables are not supported currently.\) The rest of the content can be customized.|

## Description of complex general fields: period-on-period and period-for-period

-   Minute-on-minute comparison: Assume that β is the data \(optionally average, sum, maximum, or minimum\) in the last N minutes, and α is the data generated between the Nth and 2Nth minute. The minute-on-minute comparison is the percentage increase or decrease when β is compared with α.

    ![Day-on-day Growth or Decline](../images/p174583.png)

-   Minute-for-minute hourly comparison: Assume that β is the data \(optionally average, sum, maximum or minimum\) in the last N minutes, and α is the data generated during the last N minutes in the last hour. The minute-for-minute hourly comparison is the percentage increase or decrease when β is compared with α.

    ![Growth or Decline](../images/p174585.png)

-   Minute-for-minute daily comparison: Assume that β is the data \(optionally average, sum, maximum or minimum\) in the last N minutes, and α is the data generated during the last N minutes at the same time yesterday. The minute-for-minute daily comparison is the percentage increase or decrease when β is compared with α.

    ![Growth or Decline](../images/p174586.png)


## Description of complex general fields: Alert Data Revision Strategy

You can select "Zero fill", "One fill", or "Zero fill null" \(default\). This feature is generally used to fix anomalies in data, including no data, abnormal composite metrics, and abnormal period-on-period and period-for-period comparisons.

-   Zero fill: fixes the value checked to 0.
-   One fill: fixes the value checked to 1.
-   Zero fill null: does not trigger the alert.

Scenarios:

-   Anomaly 1: no data

    User A wants to use the alert feature to monitor the page views. When User A creates the alert, User A selects Browser Monitoring Alert. User A sets the alert rule: N is 5 and the sum of the page views is at most 10. If the page is not accessed, no data is reported and no alert is sent. To solve this problem, you can select "Zero fill" as the alert data revision policy. If you do not receive any data, it considered that zero data is received. This meets the alert rule and an alert is sent.

-   Anomaly 2: abnormal composite metrics

    User B wants to use the alert feature to monitor the real-time unit price of a product. When User B creates the alert, User B selects Custom Monitoring Alert. User B sets the dataset of variable a to the current total price, and the dataset of variable b to the current total items. User B also sets the alert rule that N is 3 and the minimum value of current total price divided by current total items is at most 10. If the current total of items is 0, the value of the composite metric, current total price divided by current total items, does not exist. No alert is sent. To solve this problem, you can select "Zero fill" as the alert data revision policy. The value of the composite metric, current total price divided by current total items, is now considered to be 0. This meets the alert rule and an alert is sent.

-   Anomaly 3: abnormal period-on-period and period-for-period comparisons

    User C wants to use the alert function to monitor the CPU utilization of the node machine. When User C creates the alert, User C selects Application Monitoring Alert, and sets the alert rule: N is 3 and the average user CPU utilization of the node machine decreases by 100% compared with the previous monitoring period. If the CPU of the user fails to work in the last N minutes, α cannot be obtained. This means the period-on-period result does not exist. No alert is sent. To solve this problem, you can select the alert data revision strategy as "One fill", and consider the period-on-period comparison result as a decrease of 100%. This meets the alert rule and an alert is sent.


You can query and delete alert records in alert management.

