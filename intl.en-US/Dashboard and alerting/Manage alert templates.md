# Manage alert templates

Application Real-Time Monitoring Service \(ARMS\) provides alert templates that allow you to create alerts in batches, improving efficiency in configuring alert rules.

## Create alert templates

In addition to the default alert templates provided by ARMS, you can create custom alert templates as needed. ARMS allows you to create only two types of alert templates: browser monitoring and application monitoring.

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Template Management**.

2.  On the Alert Template Management page, click **Create Alert Template** in the upper-right corner.

    -   Click **Browser Monitoring Alert Template**. In the Create Alert Template dialog box, set all required parameters, and then click **Save**. For more information about the fields, see [Description of basic fields](#section_x9s_jul_7zb).
    -   Click **Application Monitoring Alert Template**. In the Create Alert Template dialog box, set all required parameters, and then click **Save**. For more information about the fields, see [Description of basic fields](#section_x9s_jul_7zb).
3.  Select the alert template you created in the alert template list. In the **Actions** column, click **Create Alert**. In the Create Alert dialog box, set all required parameters and click **Save**.

    Choose **Alerts** \> **Alert Policies**. On the Alert Policies page, click the Alert Rules tab. The alert rule you created appears in the alert list, indicating that you have created the alert rule by using the alert template you created.

4.  Select the alert template you created in the alert template list. In the **Actions** column, click **Batch Create Alerts**.

5.  In the Batch Create Alerts dialog box, click multiple applications in the **Unselected** section to add them to the **Selected** section. Click **Save**. In the Note dialog box, click **OK**.

    Choose **Alerts** \> **Alert Policies**. On the Alert Policies page, click the Alert Rules tab. The alert rules you created in batches appear in the alert list, indicating that you have created the alert rules in batches by using the alert template you created.


## Manage alert templates

You can enable or disable the Auto-Generation feature of an alert template, as well as edit, delete, and copy the alert template.

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Template Management**.

2.  Find the target alert template in the alert template list, and click the buttons in the **Actions** column as needed.

    -   To automatically create alert rules for a new application, click **Enable Auto-Generation**. In the Stop dialog box, click **OK**. If you do not need to automatically create alert rules for the new application, click **Disable Auto-Generation**. In the Stop dialog box, click **OK**.

        **Note:** For a newly created alert template, the Auto-Generation feature is enabled by default.

    -   To edit an alert template, click **Edit**. In the Edit Alert Template dialog box, edit the alert template, and click **Save**.
    -   To delete an alert template, click **Delete**. In the Delete dialog box, click **Delete**.
    -   To copy an alert template, click **Copy**. In the Edit Alert Template dialog box, edit the alert template, and click **Save**.

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

[Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md)

[t1861482.md\#](/intl.en-US/Dashboard and alerting/Tutorials/Create common alarm rules.md)

