# Create a contact

When an alert rule is triggered, notifications are sent to the contact group that you specified. Before you create a contact group, you must create contacts. When you create a contact, you can specify a mobile number and an email address on which the contact can receive notifications. You can also provide the webhook URL of a DingTalk chatbot that can be used to automatically send alert notifications.

To add a DingTalk chatbot as a contact, you must first obtain the webhook URL of the chatbot. For more information, see [Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and Alerting/Configure a DingTalk chatbot to send alert notifications.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane of the console, choose **Alerts** \> **Contacts**.

3.  On the **Contact** tab, click **New contact** in the upper-right corner.

4.  In the **New contact** dialog box, edit the contact information, specify whether to receive system notifications, and click **OK**.

    -   To add a contact, set the **Name**, **Mobile phone number** and **Mailbox** parameters.

        **Note:** You must set the Mobile phone number parameter, the Mailbox parameter, or both. Each mobile number or email address can be used for only one contact. You can create a maximum of 100 contacts.

    -   To add a DingTalk chatbot, enter the name and the webhook URL of the chatbot.

        **Note:** For information about how to obtain the webhook URL of a DingTalk chatbot, see [Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and Alerting/Configure a DingTalk chatbot to send alert notifications.md).


## What to do next



-   To search for contacts, select **Name**, **Cell phone number**, or **Email** from the drop-down list on the Contact tab. Enter a complete or partial contact name, mobile phone number, or email address in the search box, and then click theicon.
-   To edit a contact, click **Editing** in the **Operation** column corresponding to the contact, edit the information in the Edit contacts dialog box, and then click **OK**.
-   To delete a contact, click **Delete** in the **Operation** column corresponding to the contact, and then click **OK** in the message that appears.
-   To delete multiple contacts at a time, select the contacts, click **Batch delete** in the lower part of the Contact tab, and then click **OK** in the message that appears.

**Related topics**  


[Create a contact group](/intl.en-US/Dashboard and Alerting/Create a contact group.md)

[Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and Alerting/Configure a DingTalk chatbot to send alert notifications.md)

[Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md)

[Manage alerts](/intl.en-US/Dashboard and Alerting/Manage alerts.md)

