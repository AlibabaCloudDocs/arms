# 将 ARMS 页面嵌入自建 Web 应用 {#task_1546762 .task}

如需在自建 Web 应用中免登录查看 ARMS 控制台的页面，您可将 ARMS 控制台嵌入自建 Web 应用，以此避免系统间的来回切换。

本教程的准备工作包括创建 RAM 用户、创建 RAM 角色以及为其赋予相应权限。创建 RAM 角色时，请根据需要为 RAM 角色赋予权限：

-   如需添加 ARMS 的完整权限，则添加 AliyunARMSFullAccess。
-   如需添加 ARMS 的只读权限，则添加 AliyunARMSReadOnlyAccess。

为了快速入门，您可以下载并使用[示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/embedPage.zip)。

## 教程概述 {#section_9yd_9lb_77u .section}

**预期结果**

参照本教程的方法进行实际操作后将实现以下效果：

-   可登录您的自有系统并浏览嵌入的应用列表、应用详情、调用查询等页面。
-   可隐藏 ARMS 控制台页面的顶部导航栏和左侧导航栏。
-   可通过访问控制 RAM 系统控制操作权限，例如将完整权限改为只读权限等。

**访问流程**

使用本教程所述方法访问 ARMS 控制台页面的流程如图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227554/156507188154445_zh-CN.png)

## 准备工作：创建 RAM 用户并添加权限 {#section_56j_qp2_kgp .section}

首先使用阿里云账号（主账号）创建 RAM 用户并为其添加调用 STS 服务扮演 RAM 角色的权限。

1.  登录 [RAM 控制台](http://ram.console.aliyun.com)，在左侧导航栏中选择**人员管理** \> **用户**，并在用户页面上单击**新建用户**。
2.  在新建用户页面的**用户账号信息**区域框中，输入**登录名称**和**显示名称**。在**访问方式**区域框中，勾选**编程访问**，并单击**确认**。 

    ![Create RAM User](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156507188154440_zh-CN.png)

    **说明：** RAM 会自动为 RAM 用户创建 AccessKey（API 访问密钥）。出于安全考虑，RAM 控制台只提供一次查看或下载 AccessKeySecret 的机会，即创建 AccessKey 时，因此请务必将 AccessKeySecret 记录到安全的地方。

3.  在手机验证对话框中单击**获取验证码**，并输入收到的手机验证码，然后单击**确定**。 创建的 RAM 用户显示在用户页面上，但此时没有任何权限。
4.  在用户页面上找到创建好的用户，单击**操作**列中的**添加权限**。
5.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略 AliyunSTSAssumeRoleAccess，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。 

    ![Add Permission For User](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156507188154441_zh-CN.png)

6.  在**添加权限**的**授权结果**页面上，查看授权信息摘要，并单击**完成**。

## 准备工作：创建 RAM 角色并添加权限 {#section_qcc_ejh_ix5 .section}

接下来创建 RAM 角色并为其添加访问控制台的权限。上一步创建的 RAM 用户将会扮演该 RAM 角色访问控制台。

1.  登录 [RAM 控制台](http://ram.console.aliyun.com)，在左侧导航栏中单击 **RAM 角色管理**，并在 RAM 角色管理页面上单击**新建 RAM 角色**。
2.  在**新建 RAM 角色**面板中执行以下操作并单击**确定**。 
    1.  在**选择类型**页面的**当前可信实体类型**区域框中选择**阿里云账号**，并单击**下一步**。
    2.  在**配置角色**页面的**角色名称**文本框内输入 RAM 角色名称，并单击**完成**。
    3.  在**创建完成**页面上单击**为角色授权**。
3.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。 

    **说明：** 请搜索并添加背景信息中所述的权限。

4.  在**添加权限**面板的**授权结果**页面上，查看授权信息摘要，并单击**完成**。

## 步骤一：获取临时 AccessKey 和 Token {#section_kq4_dae_aqn .section}

登录自建 Web 后，在 Web 服务端调用 STS [AssumeRole](../intl.zh-CN/API 参考（STS）/操作接口/AssumeRole.md#) 接口获取临时 AccessKey 和 Token，即临时身份。请选择一种方式调用该接口：

-   通过 [OpenAPI](https://api.aliyun.com/#/?product=Sts&api=AssumeRole) 在线调用。
-   通过 [Java SDK](../intl.zh-CN/SDK参考/SDK参考（RAM）/Java SDK.md#) 调用。

请注意，在示例代码中，您首先需要将以下参数替换为真实的值。

``` {#d7e836}
String akId = "<accessKeyId>";
String ak = "<accessKeySecret>";
String roleArn = "<roleArn>";
```

其中，<accessKeyId\> 和 <accessKeySecret\> 是准备工作中创建的 RAM 用户的 AccessKeyId 和 AccessKeySecret。

![Example AccessKey](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156507188254442_zh-CN.png)

<roleArn\> 是准备工作中创建的 RAM 角色的标识 ARN，可在 RAM 控制台的 RAM 角色基本信息页面获取。

![Example ARN](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156507188254443_zh-CN.png)

## 步骤二：获取登录 Token {#section_q6b_i3y_tpi .section}

在通过 STS AssumeRole 接口获取临时 AccessKey 和 Token 后，调用登录服务接口获取登录 Token。

**说明：** STS 返回的安全 Token 中可能包含特殊字符，请对特殊字符进行 URL 编码后再输入。

请求样例：

``` {#d7e869}
http://signin.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<STS 返回的临时 AccessKeyId>
    &AccessKeySecret=<STS 返回的临时 AccessKeySecret>
    &SecurityToken=<STS 返回的安全 Token>
    &TicketType=mini
```

## 步骤三：生成免登录链接 {#section_vhx_2w5_ww4 .section}

利用获取到的登录 Token 与待嵌入的 ARMS 控制台页面链接生成免登录访问链接，以最终实现在自建 Web 中免登录访问 ARMS 控制台页面的目的。

**说明：** 由于 Token 有效期为 3 小时，建议在自建 Web 应用中将链接设置为每次请求时生成新登录 Token。

1.  在 ARMS 控制台获取待嵌入的控制台页面链接。例如杭州地域的应用列表页面的链接为： 

    ``` {#codeblock_ldy_6ue_8u2}
    https://arms.console.aliyun.com/?hideTopbar=true&hideSidebar=true#/tracing/list?regionNo=cn-hangzhou
    ```

    **说明：** 将 hideTopbar 设为 true 表示隐藏顶部导航栏，将 hideSidebar 设为 true 表示隐藏左侧导航栏。

2.  利用步骤二中获取到的登录 Token 与 ARMS 控制台页面链接生成免登录访问链接。 请求样例： 

    ``` {#codeblock_wxo_dxy_09j}
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<登录失效跳转的地址，一般配置为自建 Web 配置 302 跳转的 URL>
        &Destination=<ARMS 控制台页面链接>
        &SigninToken=<获取到的登录 Token>
    ```


本教程的示例代码基于 Java SDK，以嵌入 ARMS 控制台的应用列表为例。

[获取示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/embedPage.zip)

