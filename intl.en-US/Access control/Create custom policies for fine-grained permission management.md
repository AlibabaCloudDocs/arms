---
keyword: [custom policy, fine-grained permission management, RAM]
---

# Create custom policies for fine-grained permission management

You can create custom permission policies related to Application Real-Time Monitoring Service \(ARMS\) and grant Resource Access Management \(RAM\) users the read and write permissions on some applications monitored by ARMS. In addition, you can implement fine-grained permission management based on application names.

-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md)
-   [Enable RAM](/intl.en-US/Pricing/Billing.md)
-   [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md)

ARMS provides the following system permission policies:

-   **AliyunARMSFullAccess**: ARMS full access permission
-   **AliyunARMSReadOnlyAccess**: ARMS read-only permission

## Step 1: Create a custom permission policy related to ARMS

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Permissions** \> **Policies**.

2.  On the Policies page, click **Create Policy**.

3.  On the Create Custom Policy page, set the following parameters and click **OK**.

    1.  In the **Policy Name** field, enter a policy name, for example, arms-child-armsapplimit-policy.

    2.  Set **Configuration Mode** to **Script**.

    3.  In the **Policy Document** section, enter the policy content. For more information, see [Policy structure and syntax](/intl.en-US/Policy Management/Policy language/Policy structure and syntax.md).

        For example, you can use the following statements to grant a RAM user the read and write permissions on the applications prefixed with demo in the China \(Hangzhou\) region and the applications prefixed with arms in all regions that are monitored by ARMS.

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "arms:*",
                    "Resource": [
                        "acs:arms:cn-hangzhou:*:armsapp/demo*",
                        "acs:arms:*:*:armsapp/arms*"
                    ]
                },
                {
                    "Effect": "Allow",
                    "Action": "arms:*",
                    "Resource": [
                        "acs:arms:*:*:arms"
                    ]
                }
            ],
            "Version": "1"
        }
        ```


## Step 2: Add the custom policy related to ARMS application monitoring to a RAM user

1.  In the left-side navigation pane, choose **Identities** \> **Users**.

2.  On the Users page, click the target user in the **User Logon Name/Display Name** column.

3.  On the Basic Information page, click the Permissions tab.

4.  On the Individual tab, add a custom permission policy for the RAM user.

    -   If the individual permission list contains the **AliyunARMSFullAccess** or **AliyunARMSReadOnlyAccess** system policy, click **Remove Permission** in the **Actions** column on the right. In the remove permission dialog box, click **OK**. After you remove all policies, click **Add Permissions**.
    -   If the individual permission list contains no policy, click **Add Permissions**.
5.  In the Add Permissions pane, select **Custom Policy** in the **Select Policy** section, and enter the name of the custom policy that you created in [step 1](#section_56q_4wg_dob). Then, in the **Authorization Policy Name** column, select the policy that was returned in the search result, click **OK**, and then click **Complete**.


**Related topics**  


[Overview](/intl.en-US/Access control/Overview.md)

[What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)

[Terms](/intl.en-US/Product Introduction/Terms.md)

[Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md)

[Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md)

[Log on to the console as a RAM user](/intl.en-US/RAM User Management/Log on to the console as a RAM user.md)

