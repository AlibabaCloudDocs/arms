# Create a contact

When an alert rule is triggered, notifications are sent to the contact group that you specified. Before you create a contact group, you must create contacts. When you create a contact, you can specify a mobile number and an email address to which notifications are sent. You can also provide the webhook URL of a DingTalk chatbot that can be used to automatically receive alert notifications.

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane of the console, choose **Alerts** \> **Contacts**.

3.  On the **Contact** tab, click **New contact** in the upper-right corner.

4.  In the **New contact** dialog box, enter a contact name, enter the mobile number, email address, or webhook URL of a DingTalk chatbot for the contact, specify whether to receive system notifications, and then click **OK**.

    **Note:**

    -   You must set at least one of the Mobile phone number, Mailbox, and DingTalk robot parameters. Each mobile number or email address can be used for only one contact.
    -   You can create a maximum of 100 contacts within your Alibaba Cloud account.
    -   For information about how to obtain the webhook URL of a DingTalk chatbot, see [Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and Alerting/Configure a DingTalk chatbot to send alert notifications.md).

## What to do next



After you create contacts, you can search for, edit, and delete the contacts on the Contact Management page.

-   To search for contacts, on the Contact tab, select **Name**, **Cell phone number**, or **Email** from the drop-down list next to the search box. Enter a complete or partial contact name, mobile phone number, or email address in the search box, and then click the searchicon.
-   To edit a contact, click **Editing** in the **Operation** column corresponding to the contact, edit the information in the Edit contacts dialog box, and then click **OK**.
-   To delete a contact, click **Delete** in the **Operation** column corresponding to the contact. In the message that appears, click **OK**
-   To delete multiple contacts at a time, select the contacts that you want to delete, and click **Batch delete**. In the message that appears, click **OK**.

**Related topics**  


[Create a contact group](/intl.en-US/Dashboard and Alerting/Create a contact group.md)

[Configure a DingTalk chatbot to send alert notifications](/intl.en-US/Dashboard and Alerting/Configure a DingTalk chatbot to send alert notifications.md)

[Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md)

[Manage alerts](/intl.en-US/Dashboard and Alerting/Manage alerts.md)

