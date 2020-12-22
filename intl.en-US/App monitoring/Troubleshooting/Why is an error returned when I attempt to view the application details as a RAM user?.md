# Why is an error returned when I attempt to view the application details as a RAM user?

## Problem description

When I attempt to view the details of an application on the application monitoring page of the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home) as a RAM user, the following error message appears: **"Sorry, you do not have permissions to perform the operation"**.

## Cause

By default, an Alibaba Cloud account has full access to the app resources created by the account. However, new RAM users do not have full access to such resources.

## Solution

You must grant relevant permissions on the resources to the RAM user by using RAM authorization.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Permissions** \> **Policies**.

2.  On the Policies page, click **Create Policy**.

3.  On the Create Custom Policy page, set the following parameters and click **OK**.

    1.  Enter a policy name in the **Policy Name** field. Example: ARMSAppReadAccess.

    2.  Set **Configuration Mode** to **Script**.

    3.  In the **Policy Document** field, enter the following policy document:

        -   Policy content: read-only permission

            ```
            {
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Action": "emasha:View*",
                        "Resource": "*"
                    }
                ],
                "Version": "1"
            }
            ```

        -   Policy content: management permission

            ```
            {
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Action": "emasha:*",
                        "Resource": "*"
                    }
                ],
                "Version": "1"
            }
            ```

4.  In the left-side navigation pane, choose **Identities** \> **Users**.

5.  In the **Select Policy** section of the **Add Permissions** panel, click **Custom Policy**. Enter the keyword of the policy that you want to add in the search box and click the policy name to add it to the **Selected** list. Click **OK**.

    The **"Succeed"** message is returned on the **Add Permissions** panel.


