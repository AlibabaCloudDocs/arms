# Create an alert contact

If an alert rule of Tracing Analysis is triggered, notifications are sent to the specified contact group. Before you create a contact group, you must create a contact. When you create a contact, you can specify a mobile phone number and email address for the contact to receive notifications. You can also specify the webhook URL of a DingTalk chatbot to automatically receive alert notifications.

[Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and alerting/Configure a DingTalk chatbot to send alert notifications.md): The webhook URL of a DingTalk chatbot is obtained if you need to add the chatbot as a contact.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alert History** \> **Alert Contacts**.

3.  On the **Contacts** tab, click **Create Contact** in the upper-right corner.

4.  In the **Create Contact** dialog box, enter the contact information.

    -   To add a contact, you must set the **Name**, **Phone Number**, and **Email** parameters.

        **Note:** The phone number and email address cannot be left blank at the same time. Each phone number or email address must be used for only one contact. You can create a maximum of 100 contacts.

    -   To add a DingTalk chatbot, enter the name and the webhook URL of the chatbot.

        **Note:** For more information about how to obtain the webhook URL of a DingTalk chatbot, see [Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and alerting/Configure a DingTalk chatbot to send alert notifications.md).


-   To search for contacts, on the Contacts tab, select **Name**, **Phone Number**, or **Email** in the drop-down list, enter the entire or a part of the selected name, phone number or email in the search box, and then click **Search**.
-   To modify a contact, click **Edit** in the **Actions** column of the contact. In the Update Contact dialog box, modify the information and click **OK**.
-   To delete a single contact, click **Delete** in the **Actions** column of the contact. In the Delete message, click **Delete**.
-   To delete multiple contacts, select the contacts that you want to delete, click **Batch Delete Contacts**. In the Note message, click **OK**.

**Related topics**  


[Manage alerts](/intl.en-US/Operations in the Console/Alert management/Manage alerts.md)

