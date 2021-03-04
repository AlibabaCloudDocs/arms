# Use RAM roles to access resources across Alibaba cloud accounts

Use the Alibaba Cloud account of enterprise A to create A RAM role, authorize this role, and assign this role to Enterprise B. You can use the Alibaba Cloud account of Enterprise B or the corresponding RAM users to access the Alibaba Cloud resources of Enterprise A.

## Background

Assume that Enterprise A has purchased multiple types of cloud resources to carry out its businesses and needs to grant Enterprise B the permission to carry out certain businesses on behalf of Enterprise A. In this case, you can use the resource access management \(RAM\) role to perform this task. A RAM role does not have a specific logon password or AccessKey pair. A RAM user can be used only after the RAM user is assumed by a trusted entity. To meet the needs of enterprise A, you can perform the following operations:

1.  Create A RAM role for enterprise A
2.  Enterprise A attaches the required permissions to the RAM role
3.  Enterprise B creates a RAM user
4.  Enterprise B adds AliyunSTSAssumeRoleAccess permissions
5.  A RAM user of Enterprise B uses the console or API to access the resources of Enterprise A.

The following table lists the ARMS system permission policies that can be attached to a RAM role.

-   AliyunARMSFullAccess: ARMS full permission
-   AliyunARMSReadOnlyAccess: ARMS read-only permission.

## Step 1: Create A RAM role for enterprise A

You need to use the Alibaba Cloud account of enterprise A to log on to the RAM console and create A RAM role.

1.  Login [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **RAM roles**, and in RAM roles page, click **create a RAM role**.
2.  In **create a RAM role** in the panel, do the following and click **close**.
    1.  In **current trusted entity type** area box, select **alibaba Cloud account**, and click **next Step**.
    2.  In **RAM role name** enter a RAM role name in the text box. **Select Alibaba Cloud account** area box, select **other Alibaba Cloud account** and enter the cloud account of Enterprise B in the textbox. Then click **complete**.

        **Note:** The name of the RAM role can contain letters, digits, and hyphens \(-\). It can be up to 64 characters in length.


## Step 2: enterprise A attaches the required permissions to the RAM role

A newly created ram role does not have any permissions. Therefore, enterprise A must grant permissions to this role.

1.  In [RAM console](http://ram.console.aliyun.com) in the left-side navigation pane, choose **RAM roles**.
2.  In RAM roles click the target role on the page. **Operation** column in the **add permissions**.
3.  In **add permissions** panel's **select permissions** in the left-side navigation pane, search for the policy by keyword, and click the Policies tab to add it to **selected** list, and then click **confirm**.

    **Note:** For more information about the permissions that you can add, see the background information.

4.  In the **Authorization Result** section of the **Add Permissions** pane, view the authorized permission information, and click **Complete**.

## Step 3: Enterprise B creates a RAM user

Use the Alibaba Cloud account of Enterprise B to log on to the RAM console and create a RAM user.

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

## Step 4: Enterprise B attaches permissions to the RAM users

Enterprise B must add AliyunSTSAssumeRoleAccess to allow A RAM user to assume A RAM role created by Enterprise A.

1.  In [RAM console](http://ram.console.aliyun.com) in the left-side navigation pane, choose **personnel Management** \> **user**.
2.  In user to find the target user, click **operation** column in the **add permissions**.
3.  In **add permissions** panel's **select permissions** area, search by keyword AliyunSTSAssumeRoleAccess policy, and click the policy to add it to the **selected** list, and then click **confirm**.
4.  On the **Add Permissions** page, view the authorization information summary in the **Authorization Result** section, and then click **Finished**.

## What to do next

After completing the preceding operations, the RAM users of Enterprise B can log on to the console to access the cloud resources of Enterprise A or call API operations as follows.

-   Log on to the console to access the cloud resources of Enterprise A.
    1.  Open in browser [the logon page for RAM users](https://signin.aliyun.com/login.htm).
    2.  In RAM user logon page, enter the RAM user logon name, and click **next Step**, and enter the RAM user password, and then click **login**.

        **Note:** The logon name of the RAM user is in the format of <$username\>@<$AccountAlias\> or <$username\>@<$AccountAlias\>.onaliyun.com. <$AccountAlias\> is the account alias. If no account alias is set, the value defaults to the ID of the Alibaba cloud account.

    3.  On the RAM user center page, move the pointer to the portrait in the upper-right corner and click **Switch Role**.
    4.  In alibaba Cloud-role switch page, enter the name of Enterprise A's **enterprise alias** or **default domain** and **role name**, and then click **switch**.
    5.  Perform operations on the Alibaba Cloud resources of Enterprise A.
-   Use A RAM user of Enterprise B to access the cloud resources of enterprise A through APIs

    To use A RAM user of Enterprise B to access the cloud resources of Enterprise A by calling API operations, ensure that the code contains the RAM user's AccessKeyId, AccessKeySecret, and SecurityToken \(temporary security token\).


**Related topics**  


[Overview](/intl.en-US/Access control/Overview.md)

[What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)

[Terms](/intl.en-US/Product Introduction/Terms.md)

[RAM role overview](/intl.en-US/RAM Role Management/RAM role overview.md)

[Create a RAM role for a trusted Alibaba Cloud account](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud account.md)

[Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md)

[Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md)

[Log on to the console as a RAM user](/intl.en-US/RAM User Management/Log on to the console as a RAM user.md)

