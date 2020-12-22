# Configure a DingTalk chatbot alert

After you configure DingTalk chatbot alerts, you can specify DingTalk groups to receive alert notifications. This topic describes how to configure a DingTalk chatbot alert.

## Add a DingTalk chatbot and obtain a webhook URL

Perform the following steps to add a custom DingTalk chatbot and obtain the webhook URL:

1.  Run the DingTalk client on a PC, click to enter the DingTalk group to which you want to add an alert chatbot, and then click the Group Settings icon in the upper-right corner.

2.  In the **Group Settings** panel, click **Group Assistant**.

3.  In the **Group Assistant** panel, click **Add Robot**.

4.  In the **ChatBot** dialog box, click the **+** icon in the **Add Robot** card, and then click **Custom**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43302.png)

5.  In the **Robot details** dialog box, click **Add**.

6.  In the Add Robot dialog box, edit the profile picture, enter a name, select at least one of the options in the **Security Settings** section, and then select **I have read and accepted DingTalk Custom Robot Service Terms of Service**. Click **Finished**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43303.png)

7.  In the Add Robot dialog box, click **Copy** to save the webhook URL of the chatbot, and then click **Finished**.

    ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43304.png)


## Add the webhook URL to a contact and set the alert handler

1.  Create or edit a contact, and then enter the webhook URL of the robot in the **DingTalk robot** field. For more information, see [Create a contact](/intl.en-US/Dashboard and alerting/Create contacts.md).

2.  Create or edit a contact group, and then add contacts to the contact group after you add the webhook URL of the DingTalk chatbot to the contacts. For more information, see [Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md).

3.  Create or edit a dispatch rule, select the contact or contact group from the **Handler** drop-down list, and then select **DingTalk** in the **Notification method** section. Make sure that you have added the webhook URL of the DingTalk chatbot to the contact or contact group. For more information, see [Configure an alert dispatch policy]().


A DingTalk chatbot alert is configured. If the alert is triggered, you will receive an alert notification in the specified DingTalk group. The following figure shows an alert notification.

