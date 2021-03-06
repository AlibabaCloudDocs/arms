# 借助RAM用户实现分权

借助访问控制RAM的RAM用户，您可以实现权限分割的目的，按需为RAM用户赋予不同权限，并避免因暴露阿里云账号密钥造成的安全风险。

出于安全考虑，您可以为阿里云账号创建RAM用户，并根据需要为这些RAM用户赋予不同的权限，这样就能在不暴露阿里云账号密钥的情况下，实现让RAM用户各司其职的目的。在本文中，假设企业A希望让部分员工处理日常运维工作，则企业A可以创建RAM用户，并为RAM用户赋予相应权限，此后员工即可使用这些RAM用户登录控制台或调用API。

链路追踪支持的系统权限策略如下所示。

|权限策略|类型|说明|
|----|--|--|
|AliyunTracingAnalysisFullAccess|系统|链路追踪的完整权限|
|AliyunTracingAnalysisReadOnlyAccess|系统|链路追踪的只读权限|

## 步骤一：创建RAM用户

首先需要使用阿里云账号登录RAM控制台并创建RAM用户。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中选择**人员管理** \> **用户**，并在用户页面单击**创建用户**。
2.  在创建用户页面的**用户账号信息**区域，输入**登录名称**和**显示名称**。

    **说明：** 登录名称中允许使用小写英文字母、数字、英文句号（.）、下划线（\_）和短划线（-），长度不超过128个字符。显示名称不可超过24个字符或汉字。

3.  （可选）如需一次创建多个用户，则单击**添加用户**，并重复上一步。
4.  在**访问方式**区域，选中**控制台密码登录**或**编程访问**，并单击**确定**。

    **说明：** 为提高安全性，请仅选中一种访问方式。

    -   如果选中**控制台密码登录**，则完成进一步设置，包括自动生成默认密码或自定义登录密码、登录时是否要求重置密码，以及是否开启MFA多因素认证。
    -   如果选中**编程访问**，则RAM会自动为RAM用户创建AccessKey（API访问密钥）。

        **说明：** 出于安全考虑，RAM控制台只提供一次查看或下载AccessKeySecret的机会，即创建AccessKey时，因此请务必将AccessKeySecret记录到安全的地方。

5.  在手机验证对话框中单击**获取验证码**，并输入收到的手机验证码，然后单击**确定**。创建的RAM用户显示在用户页面。

## 步骤二：为RAM用户添加权限

在使用RAM用户之前，需要为其添加相应权限。

1.  在[RAM控制台](http://ram.console.aliyun.com)左侧导航栏中选择**人员管理** \> **用户**。
2.  在用户页面找到需要授权的用户，单击**操作**列中的**添加权限**。
3.  在**添加权限**面板的**选择权限**区域，通过关键字搜索需要添加的权限策略 ，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

    **说明：** 可添加的权限参见背景信息部分。

4.  在**添加权限**的授权结果页面，查看授权信息摘要，并单击**完成**。

## 后续步骤

使用阿里云账号创建好RAM用户后，即可将RAM用户的登录名称及密码或者AccessKey信息分发给其他用户。其他用户可以按照以下步骤使用RAM用户登录控制台或调用API。

-   登录控制台
    1.  在浏览器中打开[RAM用户登录入口](https://signin.aliyun.com/login.htm)。
    2.  在RAM用户登录页面，输入RAM用户登录名称，单击**下一步**，并输入RAM用户密码，然后单击**登录**。

        **说明：** RAM用户登录名称的格式为<$username\>@<$AccountAlias\>或<$username\>@<$AccountAlias\>.onaliyun.com。<$AccountAlias\>为账号别名，如果没有设置账号别名，则默认值为阿里云账号的ID。

    3.  在子用户用户中心页面单击有权限的产品，即可访问控制台。
-   使用RAM用户的AccessKey调用API

    在代码中使用RAM用户的AccessKeyId和AccessKeySecret即可。


**相关文档**  


[访问控制概述](/intl.zh-CN/访问控制/访问控制概述.md)

