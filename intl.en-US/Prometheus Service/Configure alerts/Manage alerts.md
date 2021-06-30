# Manage alerts

ARMS Prometheus Monitoring provides out-of-the-box alert rules. On the alert configuration page, you can manage all the alert rules in your Alibaba Cloud account.

## Manage an alert rule

You can enable, disable, and edit alert rules.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar, select a region. Then, click the name of the Kubernetes cluster that you want to manage.

4.  In the left-side navigation pane, click **Alarm configuration beta**.

5.  On the **Alarm configuration beta** page, set the filter conditions or enter an alert name in the search box, and then click the **Search** icon.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

6.  Perform the following operations on the filtered alert rules in the **Actions** column:

    -   To edit an alert rule, click **Editing**. In the Edit alarm dialog box, edit the alert rule and click **OK**.

        For more information about the parameters in the Edit alarm dialog box, see [Create an alert]().

    -   To enable an alert rule that is not enabled, click **Enable** and check whether the rule is enabled in the Status column.
    -   To disable an alert rule, click **Closed** and check whether the rule is disabled in the Status column.
    ![Alarm History](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7913978061/p43290.png)


## Delete an alert rule

You can delete alerts only by using alert rules. If you delete an alert rule, all the alerts related to this rule are deleted.

1.  In the left-side navigation pane, click **Settings**. On the page that appears, click the **Rule** tab.

2.  Find the rule that you want to delete and click **Delete** in the **Actions** column.

3.  In the Confirmation message, click **Delete**.


**Related topics**  


[Create an alert]()

[Create a contact](/intl.en-US/Dashboard and Alerting/Create a contact.md)

[Create a contact group](/intl.en-US/Dashboard and Alerting/Create a contact group.md)

