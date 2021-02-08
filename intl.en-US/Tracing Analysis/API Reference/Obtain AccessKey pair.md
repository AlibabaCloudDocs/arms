# Obtain AccessKey pair

This topic describes how to create an AccessKey pair for your Alibaba Cloud account or RAM user. When you call the Alibaba Cloud operations, you must use the AccessKey pair to verify your identity.

An AccessKey pair consists of an AccessKey ID and an AccessKey secret.

-   The AccessKey ID is used to verify the identity of a user.
-   The AccessKey secret is used to encrypt and verify the signature string. You must keep your AccessKey secret strictly confidential.

**Warning:** If the AccessKey pair of your Alibaba Cloud account is disclosed, your resources are at risk. We recommend that you use a RAM user to call API operations. This minimizes the risk of disclosing the AccessKey information of your Alibaba Cloud account.

1.  Log on to the [Alibaba Cloud console](https://home.console.aliyun.com/new?spm=a2c4g.11186623.2.13.b22b5f81PaDcNA#/).

2.  Move the pointer over the profile picture in the upper-right corner of the page, and click **AccessKey**.

3.  In the **Security Tips** dialog box that appears, click Continue to manage AccessKey or Get Started with Sub Users's AccessKey.

    ![Note](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6415559951/p48002.png)

4.  Obtain an AccessKey pair.

    -   Obtain an AccessKey pair of the Alibaba Cloud account.
        1.  Click **Continue to manage AccessKey**.
        2.  On the Security Management page, click **Create AccessKey**.
        3.  In the Phone Verification dialog box that appears, click Send verification code, enter the received verification code in the Verification code field, and then click **Confirm**.
        4.  In the Create User AccessKey dialog box, show **AccessKey Details** to view the AccessKey ID and AccessKey secret. Click **Save AccessKey Information**.

            ![Create AccessKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6415559951/p48003.png)

    -   Obtain an AccessKey pair of a RAM user.
        1.  Click **Get Started with Sub Users's AccessKey**.
        2.  Go to the [RAM console](https://ram.console.aliyun.com/users/new) and create a RAM user on the Create User page. Skip this step if you have created a RAM user.
        3.  In the left-side navigation pane of the [RAM console](https://ram.console.aliyun.com/users/new), choose **Identities** \> **Users**.
        4.  On the page that appears, find the target RAM user and click the user logon name. On the user details page, click the Authentication tab. In the User AccessKeys section, click **Create AccessKey**.
        5.  In the Phone Verification dialog box, click Send verification code, enter the received verification code in the Verification code field, and click **Confirm**.
        6.  In the Create AccessKey dialog box, view the AccessKey ID and AccessKey secret. To save the information of the AccessKey pair, you can click **Download CSV File** or **Copy**.

            ![Create AccessKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6415559951/p48004.png)


