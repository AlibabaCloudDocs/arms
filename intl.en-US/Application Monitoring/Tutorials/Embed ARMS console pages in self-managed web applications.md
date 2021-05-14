# Embed ARMS console pages in self-managed web applications

You can embed Application Real-Time Monitoring Service \(ARMS\) console pages in self-managed web applications. This way, you can view the pages from the applications without the need to switch between systems or log on to the ARMS console.

The operation to embed ARMS console pages in self-managed web applications brings the following benefits:

-   Allows you to log on to your own system and browse the application list, application details, and traces on the embedded ARMS console pages.
-   Hides the top navigation bar and left-side navigation pane of the ARMS console. For more information, see [Step 5: Generate a logon-free URL](#step_ejt_0s8_cjt).
-   Uses Resource Access Management \(RAM\) to manage permissions on the ARMS console. For example, you can change the full permissions to read-only permissions. For more information, see [Grant different permissions to RAM users](/intl.en-US/Access Control/Grant different permissions to RAM users.md).

## Sample code

To embed ARMS console pages in a self-managed web application, download and use the [sample code](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip).

## Step 1: Create a RAM user and grant permissions to it

Use your Alibaba Cloud account to create RAM users and grant them permissions to call Security Token Service \(STS\) to assume RAM roles.

1.  Log on to the [RAM console](http://ram.console.aliyun.com).

2.  In the left-side navigation pane, choose **Identities** \> **Users**.

3.  On the Users page, click **Create User**.

4.  On the Create User page, set the **Logon Name** and **Display Name** parameters in the **User Account Information** section, select **Programmatic Access** in the **Access Mode** section, and then click **OK**.

    **Note:** RAM automatically generates an AccessKey pair for the RAM user. Then, the RAM user can access ARMS by calling the corresponding API operations. For security reasons, the RAM console allows you to view or download the AccessKey secret only once. Therefore, when you create an AccessKey pair, you must properly save your AccessKey secret.

5.  In the Verify by Phone Number dialog box, click **Get Verification Code**, enter the verification code sent to your mobile phone, and then click **OK**.

6.  On the Users page, find the created RAM user and click **Add Permissions** in the **Actions** column.

7.  In the **Select Policy** section of the **Add Permissions** pane, enter AliyunSTSAssumeRoleAccess in the search box. Click the displayed permission policy to add it to the **Selected** list on the right side. Then, click **OK**.

    ![Add Permission For User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1744978061/p54441.png)

8.  In the **Add Permissions** pane, view the authorization information summary and click **Complete**.


## Step 2: Create a RAM role and grant permissions to it

Create a RAM role and grant it permissions to access the ARMS console. Then, the RAM user can assume the RAM role to access the ARMS console.

1.  Log on to the [RAM console](http://ram.console.aliyun.com).

2.  In the left-side navigation pane, click **RAM Roles**.

3.  On the RAM Roles page, click **Create RAM Role**.

4.  In the **Create RAM Role** pane, perform the following operations:

    1.  In the **Select Role Type** step, set the **Trusted entity type** parameter to **Alibaba Cloud Account** and click **Next**.

    2.  In the **Configure Role** step, enter a role name in the **RAM Role Name** field and click **OK**.

    3.  In the **Finish** step, click **Add Permissions to RAM Role**.

5.  In the **Select Policy** section of the **Add Permissions** pane, click System Policy or Custom Policy and enter the keyword of the policy that you want to add in the search box. Click the displayed policy to add it to the **Selected** list on the right side. Then, click **OK**.

    You can grant the following permissions on ARMS to a RAM role as needed:

    -   AliyunARMSFullAccess: the full access permissions on ARMS
    -   AliyunARMSReadOnlyAccess: the read-only permissions on ARMS
6.  In the **Add Permissions** pane, view the authorization information summary and click **Complete**.


## Step 3: Obtain the temporary AccessKey pair and STS token

Log on to the self-managed web application and call the AssumeRole operation of STS on the web server to obtain the temporary AccessKey pair and STS token. They are used as the temporary identity. For more information about the AssumeRole operation, see [AssumeRole](/intl.en-US/API Reference/API Reference (STS)/Operation interfaces/AssumeRole.md).

You can call the AssumeRole operation by using one of the following methods:

-   Use [OpenAPI Explorer](https://next.api.aliyun.com/api/Sts/2015-04-01/AssumeRole).
-   Use [RAM SDK for Java](/intl.en-US/SDK Reference/RAM SDK Reference/SDK for Java.md).

RAM SDK for Java is used as an example.

Set the following parameters when you use the SDK for Java:

```
String accessKey = "<accessKeyId>"; // The AccessKey ID of the RAM user. 
String accessSecret = "<accessKeySecret>"; // The AccessKey secret of the RAM user. 
String roleArn = "<roleArn>"; // The Alibaba Cloud Resource Name (ARN) of the RAM role. 
```

The AccessKey ID and AccessKey secret of the RAM user are provided when the RAM user is created.

Perform the following steps to obtain the ARN of the RAM role:

1.  Log on to the [RAM console](http://ram.console.aliyun.com).

2.  In the left-side navigation pane, click **RAM Roles**.

3.  In the lower part of the RAM Roles page, click the name of the RAM role whose ARN you want to obtain.

4.  On the page that appears, copy the value of the **ARN** parameter in the **Basic Information** section.

    ![Example ARN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1744978061/p54443.png)


## Step 4: Obtain the logon token

After you call the AssumeRole operation of STS to obtain the temporary AccessKey pair and STS token, call the GetSigninToken operation to obtain the logon token.

**Note:** The logon token returned by STS may contain special characters. Before you use the token, use the URL encoding method to encode the special characters.

Sample request

```
http://signin.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<The temporary AccessKey ID that is returned by STS>
    &AccessKeySecret=<The temporary AccessKey secret that is returned by STS>
    &SecurityToken=<The logon token that is returned by STS>
    &TicketType=mini
```

## Step 5: Generate a logon-free URL

Use the obtained logon token and URL of the ARMS console page that you want to embed to generate a logon-free URL. This allows you to access the ARMS console page from your self-managed web application.

**Note:** A logon token is valid for 3 hours. We recommend that you configure the URL in the self-managed web application to generate a new logon token on each request.

1.  In the ARMS console, obtain the URL of the console page that you want to embed.

    The following example is the URL of the Applications page for the China \(Shanghai\) region:

    ```
    https://arms.console.aliyun.com/apm?iframeMode=true&demo=1&pid=ac346dab-419d-48f5-b06a-e1c331c5c93e&regionId=cn-shanghai#/ac346dab-419d-48f5-b06a-e1c331c5c93e/home
    ```

    **Note:**

    -   The URL must be the console address of ARMS application monitoring. ARMS frontend monitoring is not supported.
    -   To hide the top navigation bar and the left-side navigation pane of the ARMS console, set the `iframeMode` parameter to true in the search section of the URL.
2.  Use the logon token and the URL of the ARMS console page to generate a logon-free URL for the page.

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<A URL that returns the HTTP status code 302 and redirects you to your self-managed web application>
        &Destination=<The URL of the ARMS console page>
        &SigninToken=<The obtained logon token>
    ```

3.  Use the logon-free URL to access the ARMS console page in your browser.


