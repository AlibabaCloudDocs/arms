# Create a contact group

When you create an alert rule, you can specify a contact group as the receiver of alert notifications. If the alert rule is triggered, Application Real-Time Monitoring Service \(ARMS\) sends alert notifications to the contacts in this contact group. This topic describes how to create a contact group.

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus monitoring**.

3.  In the left-side navigation pane, choose **Alarm management** \> **Contact management**.

4.  Click the contact groups tab, and click **create alarm contact group** in the upper-right corner.

5.  In the create alarm contact group dialog box, enter the **group name**, select the **alert contact**, and click **confirm**.

    **Note:** If there is no option in the list of **alarm contacts**, you need to first.


## What to do next



-   To search for a contact group, enter all or part of the contact group name in the search box on the contact group tab, and click icon.

    **Note:** Keywords are case-sensitive.

-   To edit a contact group, click the icon to the right of ![pencil_01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6573758061/p181704.png) contact group, edit the information in the edit contact group dialog box, and then click **OK**.
-   To view the contact information of a contact group, click the icon on the left of the contact group ![Down arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6573758061/p181703.png) expand the contact group.

    ![Contact Group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2217758061/p43297.png)

    **Note:** You can remove one or more contacts from an expanded contact group. To remove a contact, click **actions** in the **remove** column.

-   To delete a contact group, click the icon to the right of the contact group, and then click ![delete_01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7573758061/p181706.png) in **OK** note dialog box.

    **Note:** Before you delete a contact group, make sure that no monitoring job is running. Otherwise, features such as alerting cannot function as expected.


