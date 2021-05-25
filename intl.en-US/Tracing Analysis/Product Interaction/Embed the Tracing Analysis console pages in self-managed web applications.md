# Embed the Tracing Analysis console pages in self-managed web applications

You can embed the Tracing Analysis console pages in self-managed web applications. This can be used to view the console pages from the web applications. This way, you do not need to switch between systems or to log on to the Tracing Analysis console.

## Overview

**Expected results**

After you perform the steps in this topic, you can obtain the following results:

-   You can log on to your system and browse the embedded pages that show applications, application details, and traces.
-   You can hide the top navigation bar and left-side navigation pane of the Tracing Analysis console pages.
-   You can use Resource Access Management \(RAM\) to control access to the Tracing Analysis console pages. For example, you can change the full permissions to read-only permissions.

## Preparation: Create a RAM user and grant permissions

Use your Alibaba Cloud account to create a RAM user and authorize the RAM user to call the AssumeRole API operation of Security Token Service \(STS\).

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, choose **Identities** \> **Users**. On the Users page, click **Create User**.

2.  On the Create User page, set the **Logon Name** and **Display Name** parameters in the **User Account Information** section. Select **Programmatic Access** in the **Access Mode** section. Then, click **OK**.

    **Note:** RAM automatically generates an AccessKey pair for the RAM user. Then, the RAM user can access Tracing Analysis by calling the required API operations. For security reasons, the RAM console allows you to view or download an AccessKey secret only once. Therefore, you must keep the related AccessKey secret strictly confidential when you create an AccessKey pair.

3.  On the Users page, find the created RAM user and click **Add Permissions** in the **Actions** column.

4.  In the **Select Policy** section of the **Add Permissions** panel, enter a keyword in the search box to search for the AliyunSTSAssumeRoleAccess policy. Click the policy to add it to the **Selected** list on the right side of the section. Then, click **OK**.

5.  In the **Add Permissions** panel, view the authorization result. Then, click **Complete**.


## Preparation: Create a RAM role and grant permissions

Create a RAM role and authorize the RAM role to access the Tracing Analysis console. Then, the RAM user that is created in the preceding step can assume this RAM role to access the Tracing Analysis console.

1.  Log on to the [RAM console](http://ram.console.aliyun.com). In the left-side navigation pane, click **RAM Roles**. On the RAM Roles page, click **Create RAM Role**.

2.  In the **Create RAM Role** panel, perform the following steps and click **OK**:

    1.  In the **Select Role Type** step, set the **Trusted entity type** parameter to **Alibaba Cloud Account**. Then, click **Next**.

    2.  In the **Configure Role** step, enter a role name in the **RAM Role Name** field and click **OK**.

    3.  In the **Finish** step, click **Add Permissions to RAM Role**.

3.  In the **Select Policy** section of the **Add Permissions** panel, enter the keyword of the policy that you want to add in the search box. Click the policy to add it to the **Selected** list on the right side of the section. Then, click **OK**.

    -   To grant full permissions on Tracing Analysis to the RAM role, select the AliyunTracingAnalysisFullAccess policy.
    -   To grant read-only permissions on Tracing Analysis to the RAM role, select the AliyunTracingAnalysisReadOnlyAccess policy.
4.  In the **Add Permissions** panel, view the authorization result. Then, click **Complete**.


## Step 1: Obtain a temporary AccessKey pair and STS token

Log on to the self-managed web application. Call the [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md) API operation of STS from the application server to obtain a temporary AccessKey pair and STS token. You can call the API operation by using one of the following methods:

-   Visit [OpenAPI Explorer](https://api.aliyun.com/#/?product=Sts&api=AssumeRole).
-   See [SDK for Java](/intl.en-US/SDK Reference/RAM SDK Reference/SDK for Java.md).

You must replace the values of the following parameters in the [sample code](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip) with the actual values:

```
String akId = "<accessKeyId>";
String ak = "<accessKeySecret>";
String roleArn = "<roleArn>";
```

Replace the <accessKeyId\> and <accessKeySecret\> variables with the AccessKey ID and AccessKey secret of the RAM user that you created in earlier steps.

Replace the <roleArn\> variable with the Alibaba Cloud Resource Name \(ARN\) of the RAM role that you created. You can obtain the ARN on the details page of the RAM role in the RAM console.

## Step 2: Obtain a logon token

After you call the AssumeRole API operation of STS to obtain the temporary AccessKey pair and STS token, call the GetSigninToken API operation to obtain a logon token.

**Note:** The temporary STS token may contain special characters. Before you use the token, you must use the URL encoding method to encode the special characters.

Sample request:

```
http://signin4service.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<The temporary AccessKey ID that is returned by STS>
    &AccessKeySecret=<The temporary AccessKey secret that is returned by STS>
    &SecurityToken=<The temporary token that is returned by STS>
    &TicketType=mini
```

## Step 3: Generate a logon-free URL

Use the obtained STS token for logons and the URL of a Tracing Analysis console page that you want to embed to generate a logon-free URL. This URL can be used to access the Tracing Analysis console page from your self-managed web application. This way, you do not need to log on to the Tracing Analysis console.

**Note:** A temporary token is valid for 3 hours. We recommend that you configure the following settings for the URL in the self-managed web application: 1. Generate a new logon token on each request. 2. Redirect access to the console page by using an HTTP 302 status code.

1.  In the Tracing Analysis console, obtain the URL of the console page that you want to embed. For example, the following URL is for the Applications page for the China \(Hangzhou\) region:

    ```
    https://tracing-analysis.console.aliyun.com/?hideTopbar=true&hideSidebar=true#/appList/cn-hangzhou
    ```

    **Note:** To hide the top navigation bar and the left-side navigation pane of the Tracing Analysis console page, set the hideTopbar and hideSidebar parameters to true.

2.  Use the STS token for logons that you obtained in Step 2 and the URL of the Tracing Analysis console page to generate a logon-free URL for the page. Sample request:

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<A URL that returns HTTP status code 302 and redirects you to the self-managed website>
        &Destination=<The URL of the Tracing Analysis console page>
        &SigninToken=<The obtained logon token>
    ```


The sample code that is used in this topic is based on Tracing Analysis SDK for Java. The sample code is used to embed the Applications page of the Tracing Analysis console.

Click [here](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip) to download the sample code.

