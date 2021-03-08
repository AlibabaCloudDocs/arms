# Embed the Tracing Analysis console pages in user-created web applications

You can embed the Tracing Analysis console pages in user-created web applications. This way, you can view the console pages from the web applications without the need to switch between systems or to log on to the Tracing Analysis console.

## Overview

**Expected results**

After you perform the operations in this topic, you can obtain the following results:

-   You can log on to your own system and browse the embedded pages where you can view the applications, application details, and traces.
-   You can hide the top navigation bar and left-side navigation pane of the Tracing Analysis console pages.
-   You can use Resource Access Management \(RAM\) to manage operation permissions on the Tracing Analysis console pages. For example, you can change the full permissions to read-only permissions.

## Preparation: Create a RAM user and grant permissions

Use your Alibaba Cloud account to create a RAM user and authorize the RAM user to call the AssumeRole operation of Security Token Service \(STS\).

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Identities** \> **Users**. On the Users page, click **Create User**.

2.  On the Create User page, set the **Logon Name** and **Display Name** parameters in the **User Account Information** section. Select **Programmatic Access** in the **Access Mode** section. Then, click **OK**.

    **Note:** RAM automatically generates an AccessKey pair for the RAM user. Then, the RAM user can access Tracing Analysis by calling the corresponding API operations. For security reasons, the RAM console allows you to view or download the AccessKey secret only once. Therefore, when you create an AccessKey pair, safely record the AccessKey secret.

3.  In the Verify by Phone Number dialog box, click **Get Verification Code**, enter the verification code that is sent to your mobile phone, and then click **OK**. The created RAM user is displayed on the Users page. The RAM user has no permissions after it is created.

4.  On the Users page, find the created RAM user and click **Add Permissions** in the **Actions** column.

5.  In the **Select Policy** section of the **Add Permissions** panel, enter AliyunSTSAssumeRoleAccess in the search box. Click the displayed permission policy to add it to the **Selected** section on the right side. Then, click **OK**.

6.  In the **Add Permissions** panel, view the authorization information summary in the **Authorization** section and click **Complete**.


## Preparation: Create a RAM role and grant permissions

Create a RAM role and authorize the RAM role to access the Tracing Analysis console. Then, the RAM user that is created in the previous step can assume this RAM role to access the Tracing Analysis console.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, click **RAM Roles**. On the RAM Roles page, click **Create RAM Role**.

2.  In the **Create RAM Role** panel, perform the following operations and click **OK**:

    1.  In the **Select Role Type** step, set the **Trusted entity type** parameter to **Alibaba Cloud Account** and click **Next**.

    2.  In the **Configure Role** step, enter a role name in the **RAM Role Name** field and click **OK**.

    3.  In the **Finish** step, click **Add Permissions to RAM Role**.

3.  In the **Select Policy** section of the **Add Permissions** panel, click System Policy or Custom Policy and enter the keyword of the permission policy that you want to add in the search box. Click the displayed policy to add it to the **Selected** section on the right side. Then, click **OK**.

    -   To grant full permissions on Tracing Analysis to the RAM role, select the AliyunTracingAnalysisFullAccess policy.
    -   To grant read-only permissions on Tracing Analysis to the RAM role, select the AliyunTracingAnalysisReadOnlyAccess policy.
4.  In the **Add Permissions** panel, view the authorization information summary in the **Authorization** section and click **Complete**.


## Step 1: Obtain the temporary AccessKey pair and STS token

Log on to the user-created web application. Call the [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md) operation of STS from the application server to obtain the temporary AccessKey pair and STS token, which serve as the temporary identity. You can call the operation by using one of the following methods:

-   Use [OpenAPI Explorer](https://next.api.aliyun.com/api/Sts/2015-04-01/AssumeRole).
-   Use [SDK for Java](/intl.en-US/SDK Reference/RAM SDK Reference/SDK for Java.md).

You must replace the values of the following parameters in the sample code with the required values:

```
String akId = "<accessKeyId>";
String ak = "<accessKeySecret>";
String roleArn = "<roleArn>";
```

Set the <accessKeyId\> and <accessKeySecret\> parameters to the AccessKey ID and AccessKey secret of the RAM user that you prepare.

Set the <roleArn\> parameter to the Alibaba Cloud Resource Name \(ARN\) of the RAM role that you prepare. You can obtain the ARN on the details page of the RAM role in the RAM console.

## Step 2: Obtain the STS token for logons

After you call the AssumeRole operation of STS to obtain the temporary AccessKey pair and STS token, call the GetSigninToken operation to obtain the STS token for logons.

**Note:** The STS token may contain special characters. Before you use the STS token, use the URL encoding method to encode the special characters.

Sample request:

```
http://signin4service.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<The AccessKey ID that is returned by STS>
    &AccessKeySecret=<The AccessKey secret that is returned by STS>
    &SecurityToken=<The token that is returned by STS>
    &TicketType=mini
```

## Step 3: Generate a logon-free URL

Use the obtained STS token for logons and the URL of the Tracing Analysis console page that you want to embed to generate a logon-free URL. This URL allows you to access the Tracing Analysis console page from your user-created web application without the need to log on to the Tracing Analysis console.

**Note:** A temporary token is valid for 3 hours. We recommend that you configure the URL in the user-created web application to generate a new logon token on each request and perform a 302 redirect to the console page.

1.  In the Tracing Analysis console, obtain the URL of the console page that you want to embed. For example, the following URL is the URL of the Applications page for the China \(Hangzhou\) region:

    ```
    https://tracing-analysis.console.aliyun.com/?hideTopbar=true&hideSidebar=true#/appList/cn-hangzhou
    ```

    **Note:** To hide the top navigation bar and the left-side navigation pane of the Tracing Analysis console page, set the hideTopbar and hideSidebar parameters to true.

2.  Use the STS token for logons that you obtain in Step 2 and the URL of the Tracing Analysis console page to generate a logon-free URL for the page. Sample request:

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<The URL that returns the HTTP status code 302 and takes you to the user-created web application>
        &Destination=<The URL of the Tracing Analysis console page>
        &SigninToken=<The obtained STS token for logons>
    ```


The sample code that is used in this topic is based on Tracing Analysis SDK for Java. The sample code is used to embed the Applications page of the Tracing Analysis console.

[Obtain sample code](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip)

