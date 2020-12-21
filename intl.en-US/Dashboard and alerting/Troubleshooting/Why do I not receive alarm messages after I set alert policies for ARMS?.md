# Why do I not receive alarm messages after I set alert policies for ARMS?

## Condition

An alarm rule is set for ARMS, but no alarm message is received.

## Cause

Except for the default emergency alarm rules, ARMS alarm rules detect and judge the alarm rules every minute to generate alarm events. Alert events are classified into triggered and not triggered. Alert messages are sent only when an alert event is in the triggered state and the corresponding alert rule is not in a silent period. If you cannot receive alarm messages after setting alarm rules, troubleshoot as follows:

## Remedy

1.  In the left-side navigation pane, choose**Alarm Management** \> **Alarm policy management**, InAlarm rulesOn the tab page, enter the name of the alert you want to view in the search box, and click**Search**To view the right**Status**The column status.

    ![Tab_alarm_rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8868758061/p81473.png)

    -   If the status is**Stopped**, Click the right**Operation**Column**Start**, And inOKDialog box, click**Start**. If you still cannot receive alarm messages after you restart the alarm rule, go to the next step.[3](#step_aaw_2q7_f27).
    -   If the status is**Running**, Perform the step[3](#step_aaw_2q7_f27).
2.  Click right**Operation**Column**Alarm history**, InAlarm historyTab,Alarm event historyTab,**Trigger Status**View the trigger status of an alert event.

    **Note:** If**Trigger Status**If the triggering status of the column is green, it indicates that the alarm is not triggered. If the value is red, it indicates that the alarm has been triggered.

    -   If the trigger status is not triggered, view**Alarm content**The alarm rules displayed in the column determine whether the threshold value of the condition is incorrect. If the threshold is incorrect,Alarm rulesTab, locate the alarm rule to be modified, and click the right**Operation**Column**Edit**, InEdit alarm rulesDialog box, re-set the threshold of the alarm rule judgment condition.
    -   If the trigger status is triggered, perform the step[4](#step_ppz_b91_d1f).
    -   If no alarm event history is recorded, perform step[6](#step_dvb_363_m10).
3.  InAlarm historyTabAlarm sending HistoryTab to check whether there are alarm sending history records.

    -   If there is a record of alarm sending history but no alarm message is received, it may be restricted by the SMS operator: each mobile phone contact can receive up to 200 messages per day. After more than 200 messages, no alarm messages can be received.
    -   If no alarm sending history is recorded, the alarm may be in a silent period. Proceed with the step[5](#step_dql_in0_dfx).
4.  InAlarm sending HistoryTab, click the time interval shown in the upper right corner, and select**Last 24 hours**To check whether there are alarm sending history records in the last 24 hours.

    -   If the alarm sending history is recorded, the alarm is in a silent period.Alarm rulesTab, locate the alarm rule to be modified, and click the right**Operation**Column**Edit**, InEdit alarm rulesDialog box,**Advanced Settings**In, close**Alarm silence period switch**.

        **Note:** Open**Alarm silence period switch**If the alarm remains in the triggering state, the message will be sent again only 24 hours after the first alarm message is sent. If this function is disabled, ARMS sends an alarm every minute.

    -   If the alarm sending history is still not recorded, it may be that the correct alarm message notification method is not selected, or the contact configuration is incorrect.
        -   You need toAlarm rulesTab, locate the alarm rule to be modified, and click the right**Operation**Column**Edit**, InEdit alarm rulesSelect the correct notification method in the dialog box.
        -   Alternatively, in the left-side navigation pane, choose**Alarm Management** \> **Contact Management**, InContact ManagementTab page. Check whether the phone number, email address, URL of the DingTalk robot, and Contact Group of the contact are correctly configured. If the configuration is incorrect, configure it again.
5.  In the left-side navigation pane, choose**Application Monitoring** \> **Application List**, InApplication ListPage to check whether the application associated with the alarm rule has data.

    -   If no data is generated for the application, the application is not connected to ARMS by default, and no alarm events are generated. You need to check and solve the problem that the application has no data.
    -   If the application has data, but a certain dimension configured by the alarm rule has no data, for example, if the type of a browser monitoring alarm is page indicator, and the dimension is a specific page name, no data is reported at this time. it may be because the dimension value is entered incorrectly. You need toAlarm rulesTab, locate the alarm rule to be modified, and click the right**Operation**Column**Edit**, InEdit alarm rulesDialog box,**Dimension**Set to**Traversal**, And then refer to theAlarm event historyClick the alarm Content tab to reset the dimension value.
6.  If you still cannot receive the alarm message after performing the preceding troubleshooting steps, contact the ARMS DingTalk service account arms160804.


