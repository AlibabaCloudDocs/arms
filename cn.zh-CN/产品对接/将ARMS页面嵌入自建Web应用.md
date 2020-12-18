# 将ARMS页面嵌入自建Web应用

如需在自建Web应用中免登录查看ARMS控制台的页面，您可将ARMS控制台嵌入自建Web应用，以此避免系统间的来回切换。

本教程仅适用于ARMS应用监控。准备工作包括创建RAM用户、创建RAM角色以及为其赋予相应权限。创建RAM角色时，请根据需要为RAM角色赋予权限：

-   如需添加ARMS的完整权限，则添加AliyunARMSFullAccess。
-   如需添加ARMS的只读权限，则添加AliyunARMSReadOnlyAccess。

为了快速入门，您可以下载并使用[示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip)。

## 教程概述

**预期结果**

参照本教程的方法进行实际操作后将实现以下效果：

-   可登录您的自有系统并浏览嵌入的应用列表、应用详情、调用查询等页面，详情请参见下文。
-   可隐藏ARMS控制台页面的顶部菜单栏和左侧导航栏，详情请参见[隐藏导航栏](#step_ejt_0s8_cjt)。
-   可通过访问控制RAM控制操作权限，例如将完整权限改为只读权限等，详情请参见[添加权限](#section_qcc_ejh_ix5)。

**访问流程**

使用本教程所述方法访问ARMS控制台页面的流程如图所示。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54445.png)

## 准备工作：创建RAM用户并添加权限

首先使用阿里云账号（主账号）创建RAM用户并为其添加调用STS服务扮演RAM角色的权限。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中选择**人员管理** \> **用户**，并在用户页面上单击**新建用户**。

2.  在新建用户页面的**用户账号信息**区域框中，输入**登录名称**和**显示名称**。在**访问方式**区域框中，勾选**编程访问**，并单击**确认**。

    ![Create RAM User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54440.png)

    **说明：** RAM会自动为RAM用户创建AccessKey（API访问密钥）。出于安全考虑，RAM控制台只提供一次查看或下载AccessKeySecret的机会，即创建AccessKey时，因此请务必将AccessKeySecret记录到安全的地方。

3.  在手机验证对话框中单击**获取验证码**，并输入收到的手机验证码，然后单击**确定**。 创建的RAM用户显示在用户页面上，但此时没有任何权限。

4.  在用户页面上找到创建好的用户，单击**操作**列中的**添加权限**。

5.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略AliyunSTSAssumeRoleAccess，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

    ![Add Permission For User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54441.png)

6.  在**添加权限**的**授权结果**页面上，查看授权信息摘要，并单击**完成**。


## 准备工作：创建RAM角色并添加权限

接下来创建RAM角色并为其添加访问控制台的权限。上一步创建的RAM用户将会扮演该RAM角色访问控制台。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中单击**RAM角色管理**，并在RAM角色管理页面上单击**新建RAM角色**。

2.  在**新建RAM角色**面板中执行以下操作并单击**确定**。

    1.  在**选择类型**页面的**当前可信实体类型**区域框中选择**阿里云账号**，并单击**下一步**。

    2.  在**配置角色**页面的**角色名称**文本框内输入RAM角色名称，并单击**完成**。

    3.  在**创建完成**页面上单击**为角色授权**。

3.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

    **说明：** 请搜索并添加背景信息中所述的权限。

4.  在**添加权限**面板的**授权结果**页面上，查看授权信息摘要，并单击**完成**。


## 步骤一：获取临时AccessKey和Token

登录自建Web后，在Web服务端调用STS[AssumeRole](/cn.zh-CN/API参考/API 参考（STS）/操作接口/AssumeRole.md)接口获取临时AccessKey和Token，即临时身份。请选择一种方式调用该接口：

-   通过[OpenAPI](https://api.aliyun.com/#/?product=Sts&api=AssumeRole)在线调用。
-   通过[Java示例](/cn.zh-CN/SDK参考/SDK参考（RAM）/Java示例.md)调用。

本文以通过Java SDK调用的方式为例。

**说明：** 在[示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip)中，您需要将以下参数替换为真实值。

```
String akId = "<accessKeyId>";
String ak = "<accessKeySecret>";
String roleArn = "<roleArn>";
```

```
String accessKey = "<accessKeyId>"; //准备工作中创建的RAM用户的AccessKeyId
String accessSecret = "<accessKeySecret>"; //准备工作中创建的RAM用户的AccessKeySecret
String roleArn = "<roleArn>"; //准备工作中创建的RAM角色的标识ARN
```

其中，`<accessKeyId>`和`<accessKeySecret>`是准备工作中创建的RAM用户的AccessKeyId和AccessKeySecret。

![Example AccessKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54442.png)

`<roleArn>`是准备工作中创建的RAM角色的标识ARN，可通过以下步骤获取ARN：

1.  登录[RAM控制台](http://ram.console.aliyun.com)。

2.  在左侧导航栏单击**RAM角色管理**。

3.  在RAM角色管理页面下方的RAM角色列表中，单击[创建RAM角色并添加权限](https://help.aliyun.com/document_detail/128573.html?spm=a2c4g.11186623.6.795.42c2a4caouQMwr#d7e1355)步骤创建的RAM角色名称。

4.  在RAM角色详情页面的**基本信息**区域复制**ARN**信息。

    ![Example ARN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54443.png)


## 步骤二：获取登录Token

在通过STS AssumeRole接口获取临时AccessKey和Token后，调用登录服务接口获取登录Token。

**说明：** STS返回的安全Token中可能包含特殊字符，请对特殊字符进行URL编码后再输入。

请求样例：

```
http://signin.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<STS返回的临时AccessKeyId>
    &AccessKeySecret=<STS返回的临时AccessKeySecret>
    &SecurityToken=<STS返回的安全Token>
    &TicketType=mini
```

## 步骤三：生成免登录链接

利用获取到的登录Token与待嵌入的ARMS控制台页面链接生成免登录访问链接，以最终实现在自建Web中免登录访问ARMS控制台页面的目的。

**说明：** 由于Token有效期为3小时，建议在自建Web应用中将链接设置为每次请求时生成新登录Token。

1.  在ARMS控制台获取待嵌入的控制台页面的URL链接。例如杭州地域的应用列表页面的URL链接为：

    ```
    https://arms.console.aliyun.com/apm?iframeMode=true&demo=1&pid=ac346dab-419d-48f5-b06a-e1c331c5c93e&regionId=cn-shanghai#/ac346dab-419d-48f5-b06a-e1c331c5c93e/home
    ```

    **说明：**

    -   URL链接必须为ARMS应用监控的控制台地址，前端监控的控制台URL链接暂不支持。
    -   在URL链接的search部分添加`iframeMode=true`设置，可以隐藏ARMS控制台原有的顶部菜单栏和左侧导航栏。
2.  利用[步骤二](#sc_step_2)中获取到的登录Token与ARMS控制台页面链接生成免登录访问链接。 请求样例：

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<登录失效跳转的地址，一般配置为自建Web配置302跳转的URL>
        &Destination=<ARMS控制台页面链接>
        &SigninToken=<获取到的登录Token>
    ```


本教程的示例代码基于Java SDK，以嵌入ARMS控制台的应用列表为例。

[获取示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/embedPage.zip)

