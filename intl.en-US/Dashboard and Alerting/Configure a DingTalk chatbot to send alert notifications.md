# Configure a DingTalk chatbot to send alert notifications

After you configure a DingTalk chatbot to send notifications, you can specify DingTalk groups to receive alert notifications. This topic describes how to configure a DingTalk chatbot to send notifications.

## Add a custom DingTalk chatbot and obtain the webhook URL

Perform the following steps to add a custom DingTalk chatbot and obtain the webhook URL:

1.  Run the DingTalk client on a PC, go to the DingTalk group to which you want to add an alert chatbot, and then click the Group Settings icon in the upper-right corner.

2.  In the **Group Settings** panel, click **Group Assistant**.

3.  In the **Group Assistant** panel, click **Add Robot**.

4.  In the **ChatBot** dialog box, click the **+** icon in the **Add Robot** card. Then, click **Custom**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43302.png)

5.  In the **Robot details** dialog box, click **Add**.

6.  In the Add Robot dialog box, edit the profile picture, enter a chatbot name, and then select at least one of the options in the **Security Settings** section. Read and select **I have read and accepted DingTalk Custom Robot Service Terms of Service**. Click **Finished**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43303.png)

7.  In the Add Robot dialog box, click Copy to save the webhook URL of the chatbot and then click **Finished**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43304.png)


## Create a contact

You can create a contact or add the address to the existing contact information. In this example, a contact is created.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the Contact tab, click **New contact** in the upper-right corner.

4.  In the **New contact** dialog box, enter the Webhook URL obtained in [Add a custom DingTalk chatbot and obtain the webhook URL](#section_3tb_85o_qd0). Then, click **OK**.


## Create a contact group

You must create a contact group, because alerts triggered by an alert rule can be sent to alert contact groups instead of alert contacts.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the Contact Group tab, click **Create a contact group** in the upper-right corner.

4.  In the Create a contact group dialog box, set **Group name**, enter the contact created in [Create a contact](#section_tvi_of1_0xy) in the **Alarm contact** field, and then click **OK**.


## Create an alert

If no alert is created, create an alert first. You can configure DingTalk chatbots to send notifications for browser monitoring, application monitoring, custom monitoring, and Prometheus monitoring alerts. In this example, an application monitoring alert is created.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

3.  On the Alarm Policies page, choose **Create Alarm** \> **Application Monitoring Alarm** in the upper-right corner.

4.  In the **Create Alarm** dialog box, set the parameters and click **Save**.

    1.  Set **Alarm Name**. For example, you can enter alert on JVM-GC times in period-over-period comparison.

    2.  From the **Application Site** drop-down list, select an application.

    3.  From the **Type** drop-down list, select the type of metric that you want to monitor. For example, you can select **JVM\_Monitoring**.

    4.  Set **Dimension** to **Traverse**.

    5.  Set Alarm Rules.

        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of JVM\_FullGC increases by 100% compared with that in the previous hour.

            **Note:** To add another alert rule, click the plus sign **+** next to **Last N Minutes**.

    6.  In the **Notification Mode** section, select **Ding Ding Robot**.

    7.  Set Notification Receiver to the contact group created in [Create a contact group](#section_1kq_68o_xg6). In the **Contact Groups** list, click the name of the contact group. If the contact group appears in the **Selected Groups** list, the setting is successful.


## Edit an alert

Perform the following steps to edit an alert. In this example, an application monitoring alert is edited.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

3.  On the page that appears, find the alert that you want to edit, and click **Edit** in the **Actions** column.

4.  In the Edit Alarm dialog box, modify related parameters and click **Save**.

    1.  Change the value of Notification Mode to **Ding Ding Robot**.

    2.  Change the value of Notification Receiver to the contact group created in [Create a contact group](#section_1kq_68o_xg6). In the **Contact Groups** list, click the name of the contact group. If the contact group appears in the **Selected Groups** list, the setting is successful.


A DingTalk chatbot is configured to send notifications. When an alert is triggered, you will receive an alert notification from the specified DingTalk group. The following figure shows an alert notification.

