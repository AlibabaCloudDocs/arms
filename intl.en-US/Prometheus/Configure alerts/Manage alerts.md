# Manage alerts

Alibaba Cloud Prometheus Service provides out-of-the-box alert rules. On the alert configuration page, you can manage all the alert rules of your Alibaba Cloud account.

## Manage an alert rule

You can enable, disable, and edit alert rules.

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the top navigation bar, select a region. Then, click the name of the Kubernetes cluster that you want to manage.

3.  In the left-side navigation pane, click **Alarm configuration beta**.

4.  On the **Alarm configuration beta** page, set the filter conditions or enter an alert name in the search box, and then click the **Search** icon.

    **Note:** You can enter part of an alert name in the search box to perform a fuzzy search.

5.  In the **Actions** column, you can perform the following operations on the filtered alert rules:

    -   To edit an alert rule, click **Editing**. In the Edit alarm dialog box, edit the alert rule, and then click **OK**.

        For more information about the parameters in the Edit alarm dialog box, see [Create an alert]().

    -   To enable an alert rule that is not enabled, click **Enable**, and then view the Status column to check whether the rule is enabled.
    -   To disable an alert rule, click **Closed**, and then view the Status column to check whether the rule is disabled.
    ![Alarm History](../images/p43290.png)


## Delete an alert rule

You can delete alerts only by alert rule. If you delete an alert rule, all the alerts related to the rule are deleted.

1.  In the left-side navigation pane, click **Settings**, and then click the **Rule** tab.

2.  Find the rule that you want to delete, and then click **Delete** in the **Actions** column.

3.  In the Confirmation dialog box, click **Delete**.


**Related topics**  


[Create an alert]()

[Create a contact](/intl.en-US/Dashboard and alerting/Create contacts.md)

[Create a contact group](/intl.en-US/Dashboard and alerting/Create a contact group.md)

