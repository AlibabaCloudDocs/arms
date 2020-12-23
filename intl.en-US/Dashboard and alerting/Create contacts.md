# Create contacts

When an alert rule is triggered, notifications are sent to the contact group that you specified. Before you create a contact group, you must create contacts. When you create a contact, you can specify the mobile phone number and email address of the contact to receive notifications. You can also provide a DingTalk chatbot webhook URL used to automatically send alert notifications.

To add a DingTalk chatbot as a contact, you must obtain its webhook URL first. For more information, see [Enable DingTalk chatbot alert](/intl.en-US/Dashboard and alerting/Enable DingTalk chatbot alert.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane of the console, choose **Alerts** \> **Contacts**.

3.  On the **Contacts** tab, click **New contact** in the upper-right corner.

4.  In the **New contact** dialog box, edit the contact information, specify whether to receive system notifications, and click **OK**.

    -   To add a contact, specify the **Name**, **Mobile phone number** and **Mailbox** fields.

        **Note:** You must specify one of the Mobile phone number and Mailbox parameters. Each phone number or email address must be used for only one contact. You can create a maximum of 100 contacts.

    -   To add a DingTalk chatbot, enter the name and the webhook URL of the chatbot.

        **Note:** For more information about how to obtain the webhook URL of the DingTalk chatbot, see [Enable DingTalk chatbot alert](/intl.en-US/Dashboard and alerting/Enable DingTalk chatbot alert.md).


## Subsequent operations



-   To search for contacts, on the Contacts tab, select **Name**, **Cell phone number**, or **Email** in the drop-down list, then enter the entire or a part of the selected name, phone number or email in the search box, and click the icon.
-   To edit a contact, click **Editing** in the **Actions** column of the contact, edit the information in the Edit contacts dialog box, then click **OK**.
-   To delete a single contact, click **Delete** in the **Actions** column of the contact, then click **OK** in the message.
-   To delete multiple contacts, select the contacts, click **Batch Delete Contacts**, then click **OK** in the dialog box.

**Related topics**  


[Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md)

[Enable DingTalk chatbot alert](/intl.en-US/Dashboard and alerting/Enable DingTalk chatbot alert.md)

[Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

[Manage alerts](/intl.en-US/Dashboard and alerting/Manage alerts.md)

