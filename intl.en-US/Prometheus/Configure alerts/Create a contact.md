# Create a contact

If an alert rule is triggered, notifications are sent to the specified contact group. Before you create a contact group, you must create a contact. When you create a contact, you can specify a mobile phone number and email address for the contact to receive notifications. You can also specify the webhook URL of a DingTalk chatbot to automatically receive alert notifications.

To add a DingTalk chatbot as a contact, you must first obtain its webhook URL. For specific actions, see .

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus monitoring**.

3.  In the left-side navigation pane, choose **Alarm management** \> **Contact management**.

4.  On the **contacts** tab, click **create contact** in the upper-right corner.

5.  Edit the contact information in the **new contact** dialog box, set whether to receive system notifications, and click **OK**.

    -   To add a contact, edit the contact **name**, **mobile number**, and **email**.

        **Note:** The mobile phone number and email address cannot be left blank at the same time. Each mobile phone number or email address must be used for only one contact. You can create a maximum of 100 contacts.

    -   To add a DingTalk chatbot, enter the name and the webhook URL of the chatbot.

        **Note:** For more information about how to obtain the address of a DingTalk robot, see .


## Related operations



-   To search for a contact, on the contact tab, select the **name**, **mobile number**, or **Email** from the search drop-down box. Then, enter all or part of the contact name, mobile number, or Email in the search box. And click icon.
-   To edit a contact, click **actions** in the **edit** column corresponding to the contact. In the edit contact dialog box, edit the information and click **OK**.
-   To delete a single contact, click **actions** in the **delete** column of the right contact, and click **OK** in the prompt dialog box.
-   To delete multiple contacts, select the contacts and click **delete**. In the note dialog box that appears, click **OK**.

