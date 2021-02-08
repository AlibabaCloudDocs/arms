# Grant different permissions to RAM users

The following table describes the system policies supported by Tracing Analysis.

|Policy|Type|Description|
|------|----|-----------|
|AliyunTracingAnalysisFullAccess|System policy|Full permissions on Tracing Analysis|
|AliyunTracingAnalysisReadOnlyAccess|System policy|Read-only permissions on Tracing Analysis|

## Step 1: Create a RAM user

First, you must log on to the RAM console with your Alibaba Cloud account \(primary account\) and create a RAM user.

1.  Log on[RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose**Personnel Management** \> **User**, And inUserClick**Create a user**.

2.  InCreate a userPage**User account information**Area, enter**Logon name**And**Display name**.

    **Note:** The logon name can contain English letters, numbers, periods \(.\), underscores \(\_\), and hyphens \(-\). It cannot exceed 128 characters in length. The display name cannot exceed 24 characters.

3.  \(Optional\) if you want to create multiple users at a time, click**Add a user**, And repeat the previous step.

4.  In**Access method**Region, Select**Console password logon**Or**Programmatic access**, And click**OK**.

    **Note:** Select only one access mode to improve security.

    -   If selected**Console password logon**To complete further settings, including automatically generating the default password or customizing the logon password, whether to require password reset upon logon, and whether to enable MFA \(multi-factor authentication\).
    -   If selected**Programmatic access**, RAM automatically creates an AccessKey \(API access key\) for the RAM user.

        **Note:** For security reasons, the RAM console only allows you to view or download the AccessKeySecret once when creating an AccessKey. Therefore, you must record the AccessKeySecret in a secure place.

5.  InMobile phone verificationDialog box, click**Get verification code**, And enter the phone verification code that you received, then click**OK**.

    The created RAM user is displayed inUserPage.


## Step 2: Grant permissions to RAM users

Before using a RAM user, you must grant the corresponding permissions to the user.

1.  In[RAM console](http://ram.console.aliyun.com)In the left-side navigation pane, choose**Personnel Management** \> **User**.

2.  InUserFind the user to be authorized and click**Operation**Column**Add permissions**.

3.  In**Add permissions**Panel**Select permissions**Area, search for the policy you want to add by keyword, and click policy to add it to the right**Selected**In the list, click**OK**.

    **Note:** For more information about the permissions that can be added, see background information.

4.  In**Add permissions**Of**Authorization result**View the authorization summary, and click**Completed**.


## Subsequent steps

After creating a RAM user with an Alibaba Cloud account \(primary account\), the RAM user&\#39;s logon name, password, and AccessKey information can be distributed to other users. Other users can use RAM users to log on to the console or call APIs as follows:

-   Log on to the console
    1.  Open the RAM user logon portal in a browser[https://signin.aliyun.com/login.htm](https://signin.aliyun.com/login.htm).
    2.  InRAM user logonEnter the RAM user logon name and click**Next**, Enter the RAM user password, and then click**Log on**.

        **Note:** The RAM user logon name format is <subuser name \>@< default domain name\> or <subuser name \>@< enterprise alias\>, such as username@company-alias.onaliyun.com or username @ company-alias.

    3.  InSubuser User CenterClick a product that you are authorized to access the console.
-   Use the AccessKey of a RAM user to call APIs.

    Use the AccessKeyId and AccessKeySecret of the RAM user in the code.


**Related topics**  


[Overview](/intl.en-US/Access control/Overview.md)

