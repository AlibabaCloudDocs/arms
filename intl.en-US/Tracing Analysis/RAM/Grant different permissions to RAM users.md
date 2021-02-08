# Grant different permissions to RAM users

You can create different permissions for different RAM users, and avoid security risks caused by exposing the accesskey of your Alibaba cloud account.

For security reasons, you can create RAM users \(sub-accounts\) for your Alibaba Cloud account \(primary account\) and Grant different permissions to these sub-accounts as needed. In this way, the Ram user can assign their own responsibilities without exposing the CMK. This article assumes that Enterprise A wants to have its employees perform routine O&M work. Then, enterprise A can create A RAM user and grant this RAM user the necessary permissions. Employees can then use the RAM users to log on to the console or call API operations.

The following table describes the system policies supported by Tracing Analysis.

|Policy|Type|Description|
|------|----|-----------|
|AliyunTracingAnalysisFullAccess|System policy|Full permissions on Tracing Analysis|
|AliyunTracingAnalysisReadOnlyAccess|System policy|Read-only permissions on Tracing Analysis|

## Step 1: Create a RAM user

You need to use an Alibaba Cloud account to log on to the RAM console and create a RAM user.

1.  Login [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **personnel Management** \> **user**, and in user page, click **create User**.
2.  In create User page's **user account information** in the area box, enter **logon name** and **display name**.

    **Note:** The logon name can contain lowercase letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). The length cannot exceed 128 characters. The display name cannot exceed 24 characters or Chinese characters.

3.  \(Optional\) If you want to create multiple RAM users at a time, click **Add User**, and repeat the previous step.
4.  In **access Mode** in the area box, select **console password logon** or **programmatic access**, and click **confirm**.

    **Note:** For security purposes, select only one access mode.

    -   If **console password logon**, complete the settings. You need to determine whether to automatically generate a default password or custom password, whether to require you to reset your password, and whether to enable MFA.
    -   If **programmatic access**, RAM automatically creates an AccessKey for the RAM user \(API access key\).

        **Note:** For security reasons, the RAM console only provides the opportunity to view or download AccessKeySecret once. Therefore, the AccessKey is created. Keep the AccessKeySecret recorded in a safe place.

5.  In mobile phone verification dialog box, click **obtain verification code**, and enter the received phone verification code, and then click **confirm**. The created RAM user is displayed in user page.

## Step 2: Grant permissions to the RAM user

Before using a RAM user, you must grant permissions to the RAM user.

1.  In [RAM console](http://ram.console.aliyun.com) in the left-side navigation pane, choose **personnel Management** \> **user**.
2.  In user to find the target user, click **operation** column in the **add permissions**.
3.  In **add permissions** panel's **select permissions** in the left-side navigation pane, search for the policy by keyword, and click the Policies tab to add it to **selected** list, and then click **confirm**.

    **Note:** For more information about the permissions that you can add, see the background information.

4.  On the **Add Permissions** page, view the authorization information summary in the **Authorization Result** section, and then click **Finished**.

## What to do next

After creating RAM users with an Alibaba Cloud account, you can distribute the logon names and passwords of the RAM users or AccessKey pair information to other RAM users. Other employees can log on to the console or call an API operation with the RAM user through the following steps.

-   Log on to the console
    1.  Open in browser [the logon page for RAM users](https://signin.aliyun.com/login.htm).
    2.  In RAM user logon page, enter the RAM user logon name, and click **next Step**, and enter the RAM user password, and then click **login**.

        **Note:** The logon name of the RAM user is in the format of <$username\>@<$AccountAlias\> or <$username\>@<$AccountAlias\>.onaliyun.com. <$AccountAlias\> is the account alias. If no account alias is set, the value defaults to the ID of the Alibaba cloud account.

    3.  On the homepage of the Alibaba Cloud console, click a product with the permission to access the console.
-   Call an API operation with the RAM user's AccessKey

    Use the AccessKeyId and AccessKeySecret of the RAM user in the code.


**Related topics**  


[Overview](/intl.en-US/Access control/Overview.md)

