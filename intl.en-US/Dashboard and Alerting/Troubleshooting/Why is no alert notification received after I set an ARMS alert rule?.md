# Why is no alert notification received after I set an ARMS alert rule?

## Problem description

An Application Real-Time Monitoring \(ARMS\) alert rule has been set, but no alert notification is received.

## Possible causes

Except for default emergency alert rules, all other ARMS alert rules require that the system check whether the conditions of the alert rules are met and generate alert events at intervals of 1 minute. An alert event indicates whether an alert is triggered or not. An alert notification is sent only when an alert is triggered and the corresponding alert rule is not in a quiescent period. If you cannot receive alert notifications after you set an alert rule, perform the following steps for troubleshooting.

## Solution

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**. On the Alert Rules tab, enter the name of the alert rule that you want to view in the search box and click **Search**. View the alert rule status in the **Status** column.

    ![tab_alarm_rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8868758061/p81473.png)

    -   If the alert rule is in the **Stopped** state, click **Start** in the **Actions** column. In the OK message, click **Start**. If you still cannot receive alert notifications after you restart the alert rule, proceed with [Step 3](#step_aaw_2q7_f27).
    -   If the alert rule is in the **Running** state, proceed with [Step 3](#step_aaw_2q7_f27).
3.  Click **View Alert Detail** in the **Actions** column. On the Alert History tab, click the Alert Event History tab, and view the icon in the **Trigger** column to check the status of the alert event, which indicates whether an alert is triggered.

    **Note:** A green icon in the **Trigger** column indicates that no alert is triggered. A red icon indicates that an alert is triggered.

    -   If no alert is triggered, check whether the threshold for the alert rule is appropriate in the **Alarm Detail** column. If the threshold is inappropriate, go to the Alert Rules tab, find the alert rule, and then click **Edit** in the **Actions** column. In the Edit Alarm dialog box, specify a new threshold for the alert rule.
    -   If an alert is triggered, proceed with [Step 4](#step_ppz_b91_d1f).
    -   If no record exists in the alert event history, proceed with [Step 6](#step_dvb_363_m10).
4.  On the Alert History tab, click the Alarm Post History tab and check the alert notification records.

    -   If an alert notification record exists but you still do not receive an alert notification, the upper limit on inbound alert notifications may have been reached. Each mobile phone contact can receive up to 100 short messages per day, and each email contact can receive up to 50 emails per day. After the upper limit is reached, no more alert notifications can be received.
    -   If no alert notification record exists, the alert rule may be in a quiescent period. In this case, proceed with [Step 5](#step_dql_in0_dfx).
5.  On the Alarm Post History tab, click the date and time picker in the upper-right corner. In the list that appears, click **Last 24 Hours** to check the alert notification records in the last 24 hours.

    -   If an alert notification record exists, the alert rule is in a quiescent period. In this case, click the Alert Rules tab, find the alert rule, and then click **Edit** in the **Actions** column. In the **Advanced Configuration** section of the Edit Alarm dialog box, turn off **Alarm Quiet Period**.

        **Note:** After you turn on **Alarm Quiet Period**, if an alert stays in the triggered state, an alert notification is sent only 24 hours after the first alert notification is sent. After you turn off this switch, ARMS sends an alert notification every minute.

    -   If no alert notification record exists, the alert notification method or the contact configuration may be invalid.
        -   In this case, click the Alert Rules tab, find the alert rule, and then click **Edit** in the **Actions** column. In the Edit Alarm dialog box, select a valid notification method and a valid contact.
        -   Alternatively, in the left-side navigation pane, choose **Alerts** \> **Contacts**. On the Contact tab, check whether the mobile phone number, email address, DingTalk chatbot URL, and contact group of the contact are properly specified. If a setting is invalid, reconfigure it.
6.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the Applications page, check whether data is generated for the application that is associated with the alert rule.

    -   If no data is generated for the application, the application is not connected to ARMS and therefore no alert event is generated. In this case, check and resolve the data generation issue.
    -   If data is generated for the application but no data exists in a dimension of the alert rule, for example, no data exists in the Page\_Name dimension of a Page\_Metric frontend monitoring alert, the dimension value may be invalid. In this case, go to the Alert Rules tab, find the alert rule, and then click **Edit** in the **Actions** column. In the Edit Alarm dialog box, set the **Dimension** parameter to **Traverse**, and reconfigure the dimension value by referring to the traversal alert details displayed on the Alert Event History tab.
7.  If you still do not receive alert notifications after you perform the preceding steps, contact the ARMS DingTalk account \(ID: arms160804\) or join the ARMS DingTalk group \(ID: 30004969\) to seek help.


