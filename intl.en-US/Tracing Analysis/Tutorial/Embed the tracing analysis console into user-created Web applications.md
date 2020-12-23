# Embed the tracing analysis console into user-created Web applications

To view the tracing analysis console on the user-created Web applications page without logging on to the console, you can embed the tracing analysis console into the user-created Web application to avoid fro-switching between systems.

## Overview

**Expected results**

After you perform the operations in this topic, you can obtain the following results:

-   You can log on to your system and browse the embedded applications, application details, call query, and other pages.
-   You can hide the top navigation bar and the left-side navigation pane on the tracing analysis page.
-   You can use RAM to control operation permissions. For example, you can change full permissions to read-only permissions.

## Preparation: creating a RAM user and adding permissions

Use an Alibaba Cloud account to create a RAM user and authorize the RAM user to call STS.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Personnel management** \> **User**, and on the users page, click **New user**.

2.  On the create user page, enter a logon **user account information** name in the **logon name** and **display name** columns. In the **access mode** section, select **programmatic access**, and click **OK**.

    **Note:** RAM automatically creates an AccessKey pair for the RAM user. For security reasons, the RAM console allows you to view or download the AccessKey secret only once. Therefore, when creating an AccessKey pair, record the AccessKey secret safely.

3.  Click phone verification in the **get verification** dialog box, enter the received verification code, and then click **OK**. The created RAM user is displayed on the users page but does not have any permissions.

4.  On the userspage, find the created user and click **actions**column in The **add permissions**

5.  On the **add permissions** page, in the **select permissions** section, enter keywords to search for the policy AliyunSTSAssumeRoleAccess. Then click the policy to add it to the **selected** list on the right, and click **OK**.

6.  On the **permissions** page, view the **authorization result**, and click **complete**.


## Preparations: creating RAM roles and adding permissions

Next, create a RAM role and grant it the permission to access the tracing analysis console. The RAM User created in step 1 will assume the RAM role to access the Alibaba Cloud Console.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **RAM roles**. On the RAM roles page, click **create RAM role**.

2.  On the **create RAM role** page, perform the following operations and then click **OK**.

    1.  On the **select type** page, select **current trusted entity type** in the **Alibaba Cloud account** section, and click **next**.

    2.  On the **configure role** page, enter a RAM role name in the **role name** field, and click **create**.

    3.  On the **created** page, click **authorize role**.

3.  On the **add permissions** tab, **select permissions** from the select permissions section. Enter keywords to search for the policy to be added. Click the policy to add the policy to the **selected** list on the right. Then click **OK**.

    -   To have the full tracing permission, create AliyunTracingAnalysisFullAccess.
    -   To add the read-only permission for tracing analysis, add AliyunTracingAnalysisReadOnlyAccess.
4.  On the **add permissions** page, view the **authorization result** and click **complete**.


## Step 1: obtain the temporary AccessKey and Token

After logging on to the self-built Web server, call the STS [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md) API operation to obtain a temporary AccessKey and Token, which are temporary identities. Select a method to call the interface:

-   Call online through [OpenAPI](https://api.aliyun.com/#/?product=Sts&api=AssumeRole).
-   Through the [RAM SDK for Java](/intl.en-US/SDK Reference/RAM SDK Reference/RAM SDK for Java.md) call.

Note that in the \[sample code\] \( https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip You must replace the following parameters with actual values:

```

     String akId = "<accessKeyId>"; String ak = "<accessKeySecret>"; String roleArn = "<roleArn>"; 
   
```

Wherein the <accessKeyId\>and <accessKeySecret\>is that you created in preparations with the RAM user's AccessKeyId and AccessKeySecret.

<roleArn\> isThe ARN of the RAM role created in the preparations. You can find the ARN on the basic information page of the RAM role in the RAM console.

## Step 2: obtain a logon Token

After obtaining the temporary AccessKey and Token through the STS AssumeRole interface, call the logon service interface to obtain the logon Token.

**Note:** The security Token returned by STS may contain special characters. Therefore, encode the special characters before entering them.

Sample request

```

     http://signin4service.aliyun.com/federation?Action=GetSigninToken &AccessKeyId= <STS 返回的临时 AccessKeyId> &AccessKeySecret= <STS 返回的临时 AccessKeySecret> &SecurityToken= <STS 返回的安全 Token> &TicketType=mini 
   
```

## Step 3: Generate a logon-free URL

Use the obtained logon Token and the link to be embedded in the tracing analysis console to generate a logon free endpoint. This allows you to log on to the tracing analysis console without the need to log on to your website.

**Note:** The Token is valid for three hours. Therefore, we recommend that you set the link in the self-built Web application to generate a new logon Token upon each request and redirect the access request to the internal Web server through a 302 request.

1.  Log on to the tracing analysis console and obtain the URL of the link management console. For example, the link to the application list in the China \(Hangzhou\) region is as follows:

    ```
    
            https://tracing-analysis.console.aliyun.com/?hideTopbar=true&hideSidebar=true#/appList/cn-hangzhou 
          
    ```

    **Note:** If hideTopbar is set to true, the top navigation bar is hidden. If hideSidebar is set to true, the left-side navigation pane is hidden.

2.  Use the logon Token obtained in step 2 to generate a logon endpoint in the tracing analysis console. Sample request

    ```
    
            http://signin.aliyun.com/federation?Action=Login &LoginUrl=<address to which a 302 redirect attempt is based on a logon failure. This parameter is usually set to the URL of the user-created Web console.> &Destination=<link to the tracing console page> &SigninToken=<obtained logon Token> 
          
    ```


Log on to the user-created Web application. The following figure shows the tracing analysis page that appears:

The sample code of this topic is based on the Java SDK. The following takes the application list in the tracing analysis console as an example.

[Obtain sample code](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip)

