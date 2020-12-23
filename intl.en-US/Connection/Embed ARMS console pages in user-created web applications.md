# Embed ARMS console pages in user-created web applications

You can embed ARMS console pages in user-created web applications. This way, you can view the pages from the applications without the need to switch between systems or to log on to the ARMS console.

This tutorial applies only to ARMS application monitoring. To prepare for this tutorial, you must create a Resource Access Management \(RAM\) user, create a RAM role, and grant permissions to the RAM role. When you create a RAM role, grant permissions to the RAM role based on the following rules:

-   To grant the full permissions of ARMS, attach the AliyunARMSFullAccess policy to the role.
-   To grant the read-only permissions of ARMS, attach the AliyunARMSReadOnlyAccess policy to the role.

For a quick start, you can download and use the sample code. For more information, see [Sample code](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip).

## Overview

**Expected results**

After you perform the operations in this topic, you can obtain the following results:

-   You can log on to your own system and browse the embedded pages, such as the applications, application details, and invocation trace query pages. For more information, see the following sections in this topic.
-   You can hide the top navigation bar and left-side navigation pane of the ARMS console. For more information, see [Hide the navigation bar](#step_ejt_0s8_cjt).
-   You can use RAM to manage operation permissions on the ARMS console pages. For example, you can change the full permissions to read-only permissions. For more information, see the [Create a RAM role and grant permissions to the RAM role](#section_qcc_ejh_ix5) section in this topic.

## Preparation: creating a RAM user and adding permissions

Use an Alibaba Cloud account to create a RAM user and authorize the RAM user to call STS.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Personnel management** \> **User**, and on the users page, click **New user**.

2.  On the create user page, enter a logon **user account information** name in the **logon name** and **display name** columns. In the **access mode** section, select **programmatic access**, and click **OK**.

    **Note:** RAM automatically creates an AccessKey pair for the RAM user. For security reasons, the RAM console only allows you to view or download the AccessKeySecret once. Therefore, you must record the AccessKeySecret in a safe place when creating the AccessKey.

3.  Click phone verification in the **get verification** dialog box, enter the received verification code, and then click **OK**. The created RAM user is displayed on the users page but does not have any permissions.

4.  On the users page, locate the created user and click **actions** in the **add permissions** column.

5.  On the **add permissions** page, in the **select permissions** section, enter keywords to search for the policy AliyunSTSAssumeRoleAccess. Then click the policy to add it to the **selected** list on the right, and click **OK**.

6.  On the **permissions** page, view the **authorization result**, and click **complete**.


## Preparations: creating RAM roles and adding permissions

Next, create a RAM role and authorize it to access the console. The RAM User created in step 1 will assume the RAM role to access the console.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **RAM roles**. On the RAM roles page, click **create RAM role**.

2.  On the **create RAM role** page, perform the following operations and then click **OK**.

    1.  On the **select type** page, select **current trusted entity type** in the **Alibaba Cloud account** section, and click **next**.

    2.  On the **configure role** page, enter a RAM role name in the **role name** field, and click **create**.

    3.  On the **created** page, click **authorize role**.

3.  On the **add permissions** tab, **select permissions** from the select permissions section. Enter keywords to search for the policy to be added. Click the policy to add the policy to the **selected** list on the right. Then click **OK**.

    **Note:** Please search and add the permissions described in the background information.

4.  On the **add permissions** page, view the **authorization result** and click **complete**.


## Step 1: obtain the temporary AccessKey and Token

After logging on to the self-built Web server, call the STS [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md) API operation to obtain a temporary AccessKey and Token, which are temporary identities. Select a method to call the interface:

-   Call online through [OpenAPI](https://api.aliyun.com/#/?product=Sts&api=AssumeRole).
-   Through the [RAM SDK for Java](/intl.en-US/SDK Reference/RAM SDK Reference/RAM SDK for Java.md) call.

This topic uses the Java SDK as an example.

**Note:** In the [sample code](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip), you need to replace the following parameters with real values.

```

     String akId = "<accessKeyId>"; String ak = "<accessKeySecret>"; String roleArn = "<roleArn>"; 
   
```

```

     String accessKey = "<accessKeyId>"; // AccessKeyId String accessSecret of the RAM User created in the preparation step="<accessKeySecret>"; // AccessKeySecret String roleArn of the RAM User created in the preparation step="<roleArn>"; // ARN of the RAM role created in the preparation step 
   
```

Wherein the `<accessKeyId>`and `<accessKeySecret>`is that you created in preparations with the RAM user's AccessKeyId and AccessKeySecret.

`<roleArn> is`The ARN of the RAM role created in the preparation step. Follow these steps to obtain the ARN:

1.  Log on to the [RAM console](http://ram.console.aliyun.com).

2.  In the left-side navigation pane, choose **RAM roles**.

3.  On the RAM roles page, click [create RAM role and add permissions](https://www.alibabacloud.com/help/doc-detail/128573.htm?spm=a2o1z.12531199.0.0.13477e2c01mvaw#d7e1345).

4.  On the RAM role details page, copy the **basic information** information in the **ARN** section.


## Step 2: obtain a logon Token

After obtaining the temporary AccessKey and Token through the STS AssumeRole interface, call the logon service interface to obtain the logon Token.

**Note:** The security Token returned by STS may contain special characters. Therefore, encode the special characters before entering them.

Sample request:

```

     http://signin.aliyun.com/federation?Action=GetSigninToken &AccessKeyId= <STS返回的临时AccessKeyId> &AccessKeySecret= <STS返回的临时AccessKeySecret> &SecurityToken= <STS返回的安全Token> &TicketType=mini 
   
```

## Step 3: Generate a logon-free URL

Use the obtained logon token and URL of the ARMS console page that you want to embed to generate a logon-free URL. This allows you to access the ARMS console page from your user-created web application.

**Note:** The temporary token is valid for 3 hours. We recommend that you configure the URL in the user-created web application to generate a new logon token on each request.

1.  In the ARMS console, obtain the URL of the console page that you want to embed. For example, the URL of the Applications page for the China \(Shanghai\) region is:

    ```
    https://arms.console.aliyun.com/apm?iframeMode=true&demo=1&pid=ac346dab-419d-48f5-b06a-e1c331c5c93e&regionId=cn-shanghai#/ac346dab-419d-48f5-b06a-e1c331c5c93e/home
    ```

    **Note:**

    -   The URLs must be the URLs of Application Monitoring pages in the ARMS console. The URLs of Browser Monitoring pages in the ARMS console are not supported.
    -   To hide the top navigation bar and the left-side navigation pane of the ARMS console, set `iframeMode` to true in the search section of the URL.
2.  Use the logon token obtained in [Step 2](#sc_step_2) and the URL of the ARMS console page to generate a logon-free URL for the page. Sample request

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<A URL that returns HTTP status code 302 and takes you to the user-created website>
        &Destination=<The URL of the ARMS console page>
        &SigninToken=<The obtained logon token>
    ```


The sample code used in this topic is based on ARMS SDK for Java. The sample code is used to embed the applications page of the ARMS console.

[Obtain sample code](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip)

