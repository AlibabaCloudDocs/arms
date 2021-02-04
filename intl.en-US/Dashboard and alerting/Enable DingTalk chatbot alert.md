# Enable DingTalk chatbot alert

After enabling the DingTalk chatbot alert, you can specify DingTalk groups to receive the alert notifications. This topic describes how to enable the DingTalk chatbot alert function.

1.  Obtain the webhook URL.
    1.  Run the DingTalk client on a PC, click to enter the DingTalk group to which you want to add an alert chatbot, and click the Group Settings icon in the upper-right corner.
    2.  In the Group Settings dialog box, click **Group Assistant**.
    3.  On the Group Assistant page, click **+** icon in the **Add Robot** section, and then click **Custom**.

        ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43302.png)

    4.  In the Add Robot dialog box, edit the chatbot avatar and name, then click **Finished**.

        ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43303.png)

    5.  In the Add Robot dialog box, copy the webhook URL that the system generates for the chatbot.

        ![Add Robot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2467758061/p43304.png)

2.  On the Contact page of the console, add DingTalk chatbot as a contact. For more information on how to add a contact, see [Create contacts](/intl.en-US/Dashboard and alerting/Create contacts.md).
3.  Create a contact group, and choose the contact that you created in the previous step as the alert contact. For more information on how to create a contact group, see [Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md).
4.  Set alert rules.
    -   If you have not created an alert notification yet, create one. Select **DingTalk chatbot** as the notification mode, and set the notification receiver to the contact group that you created in [Step 3](#step3). For more information, see [Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md).
    -   If you have already created an alert notification, modify it. Select **DingTalk chatbot** as the notification mode, and set the notification receiver to the contact group that you created in [Step 3](#step3). For more information, see [Manage alerts](/intl.en-US/Dashboard and alerting/Manage alerts.md).

Now, you have enabled the DingTalk chatbot alert notifications. When an alert is triggered, you will receive an alert notification in the specified DingTalk group, For example:

