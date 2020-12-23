# Create contact groups

When creating an alert rule, you can specify a contact group as the alert notifications receiver. When the alert rule is triggered, Application Real-Time Monitoring Service \(ARMS\) sends alert notifications to the contacts in this contact group. This topic describes how to create contact groups.

You have [created contacts](/intl.en-US/Dashboard and alerting/Create contacts.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane of the console, choose **Alerts** \> **Contact Management**.

3.  On the Contact Groups tab page, click **New Contact Group** in the upper-right corner.

4.  In Create Contact Group dialog box, enter **Group Name**, select **Contact Members**, and click **OK**.

    **Note:** If there are no options in the **Contact Members** list, you need to first [Create a contact](/intl.en-US/Dashboard and alerting/Create contacts.md).


## What to do next

-   To search for a contact group, go to the Contact Groups tab, enter all or some characters of the contact group name in the search box, then click **Search**.

    **Note:** English keywords are case-sensitive.

-   To edit a contact group, click the pencil icon on the right side of the contact group, and edit the information in the Edit Contact Group dialog box.
-   To show the contacts under a contact group, click the downward arrow on the right side of a contact group to expand the group.

    ![Contact Group](../images/p43297.png "Show the contacts under a contact group")

    **Note:** You can remove one or more contacts from an expanded contact group. To remove a contact, click **Delete** in the **Actions** column of the target contact.

-   To delete a contact group, click the X icon on the right side of a contact group.

    **Note:** Before deleting a contact group, make sure that no monitoring job is running. Otherwise, alerting and other functions may be ineffective.


[Create contacts](/intl.en-US/Dashboard and alerting/Create contacts.md)

[Enable DingTalk chatbot alert](/intl.en-US/Dashboard and alerting/Enable DingTalk chatbot alert.md)

[Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

[Manage alerts](/intl.en-US/Dashboard and alerting/Manage alerts.md)

