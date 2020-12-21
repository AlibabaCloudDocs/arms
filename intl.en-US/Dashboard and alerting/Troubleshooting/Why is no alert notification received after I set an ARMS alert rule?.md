# Why is no alert notification received after I set an ARMS alert rule?

## Condition

Application Real-Time Monitoring \(ARMS\) alert rules have been set, but no alert notification is received.

## Cause

Except for default emergency alert rules, all other ARMS alert rules require that your system check for exceptions, determine the alert rule status, and generate alert events at an interval of one minute. An alert event is either triggered or not triggered. An alert notification is sent only when the alert event is triggered and the corresponding alert rule is not in a quiet period. If you cannot receive any alert notification after you set an alert rule, perform the following steps for troubleshooting.

## Solution

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**. On the Alert Rules tab, enter the target alert name in the search box, and then click **Search**. View the status in the **Status** column.

    ![tab_alarm_rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8868758061/p81473.png)

    -   If the status is **Stopped**, click **Start** in the **Actions** column. In the **OK** dialog box, click Start. If you still cannot receive any alert notifications after you restart the alert rule, proceed with step [3](#step_aaw_2q7_f27).
    -   If the status is **Running**, proceed with step [3](#step_aaw_2q7_f27).
2.  Click **View Alert Detail** in the **Actions** column. On the Alert History tab, click the Alert Event History tab, and check whether the alert event has been triggered in the **Trigger** column.

    **Note:** A green icon in the **Trigger** column indicates that the alert event is not triggered. A red icon indicates that the alert event has been triggered.

    -   If the alert event is not triggered, check whether the threshold for the alert rule is wrong in the **Alert Detail** column. If the threshold is wrong, on the Alert Rules tab, find the target alert rule, and click **Edit** in the **Actions** column. In the Edit Alert dialog box, reconfigure the threshold for the alert rule.
    -   If the alert event has been triggered, proceed with step [4](#step_ppz_b91_d1f).
    -   If no record exists in the alert event history, proceed with step [6](#step_dvb_363_m10).
3.  On the Alert History tab, click the Alert Post History tab, and check for alert post records.

    -   If an alert post record exists but you still do not receive any alert notification, the upper limit on incoming messages may have been reached. Each mobile phone contact can receive up to 100 short messages per day, and each email contact can receive up to 50 emails per day. After the upper limit is exceeded, no more alert notifications can be received.
    -   If no alert post record exists, the alert may be in a quiet period. In this case, proceed with step [5](#step_dql_in0_dfx).
4.  On the Alert Post History tab, click the time range in the upper-right corner. In the list that appears, click **Last 24 Hours** to check for alert post records in the last 24 hours.

    -   If an alert post record exists, click the Alert Rules tab, find the target alert rule, and then click **Edit** in the **Actions** column. In the **Advanced Configuration** section of the Edit Alert dialog box, turn off the **Alert Quiet Period** switch.

        **Note:** After you turn on the **Alert Quiet Period** switch, if the alert stays in the triggered state, an alert notification is sent only 24 hours after the first alert notification is sent. After you turn off this switch, ARMS sends an alert notification every minute.

    -   If the alert post record section is still empty, the alert notification method or the contact configuration may be invalid.
        -   In this case, click the Alert Rules tab, find the target alert rule, and then click **Edit** in the **Actions** column. In the Edit Alert dialog box, select a correct notification method.
        -   Alternatively, in the left-side navigation pane, choose **Alerts** \> **Contacts**. On the Contact Management tab, check whether the settings of Cell Phone Number, Email, DingTalk Robot, and Contact Group are correct. If any setting is invalid, reconfigure it.
5.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the Applications page, check whether any data is generated for the application that is associated with the alert rule.

    -   If no data is generated for the application, the application is not connected to ARMS and therefore no alert event is generated. In this case, check and solve the data generation problem.
    -   If data is generated for the application but no data exists in a dimension of the alert rule, for example, no data exists in the Page\_Name dimension of a Page\_Metric browser monitoring alert, the dimension value may be invalid. In this case, click the Alert Rules tab, find the target alert rule, and then click **Edit** in the **Actions** column. In the Edit Alert dialog box, set **Dimension** to **Traversal**, and then reconfigure the dimension value by referring to the traversal alert details displayed on the Alert Event History tab.
6.  If you still do not receive any alert notifications, contact the ARMS DingTalk account, arms160804.


