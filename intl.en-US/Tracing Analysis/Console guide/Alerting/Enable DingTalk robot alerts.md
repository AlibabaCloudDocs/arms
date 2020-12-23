# Enable DingTalk robot alerts

ARMS allows you to receive alert notifications from DingTalk groups. After enabling the DingTalk robot alert function, you can receive alert notifications from DingTalk groups. This topic describes how to enable the DingTalk robot alert function.

1.  Obtain the address of the DingTalk robot.

    1.  Run the DingTalk client on a PC, click to enter the DingTalk group to which you want to add an alert robot, and click the Group Settings icon in the upper-right corner.
    2.  In the Group Settings dialog box that appears, choose **ChatBot**.

    3.  On the ChatBot page that appears, click **+** in the **Add Robot** section, and then click **Custom**.

    4.  In the Add Robot dialog box that appears, edit the robot avatar and name, and click **Finish**.

    5.  In the **Add Robot** dialog box that appears, copy the address that the system generates for the robot.

2.  In the ARMS console, add the DingTalk robot as the contact. For more information about how to add a contact, see [Create contacts](/intl.en-US/Dashboard and alerting/Create contacts.md).

3.  Create a contact group, and add the contact that you created in the previous step as the alert contact. For more information about how to create a contact group, see [Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md).

4.  Set alert rules.

    -   If you have not created an alert job yet, create an alert first, set the notification mode to **DingTalk Robot**, and set the notification receiver to the contact group that you created in [Step 3](#step3).

    -   If you have created an alert job, click [Modify Alert Rules](/intl.en-US/Dashboard and alerting/Manage alerts.md), set the notification mode to DingTalk Robot, and set the notification receiver to the contact group that you created in [Step 3](#step3).


Now, you have enabled the DingTalk robot alert function. When an alert is triggered, you can receive the alert notification in the specified DingTalk group, for example:

