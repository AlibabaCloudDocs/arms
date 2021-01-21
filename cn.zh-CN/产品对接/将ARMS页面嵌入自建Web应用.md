# 将ARMS页面嵌入自建Web应用

如需在自建Web应用中免登录查看ARMS控制台的页面，您可将ARMS控制台嵌入自建Web应用，以此避免系统间的来回切换。

将ARMS控制台嵌入自建Web应用可以实现以下效果：

-   可登录自有系统并浏览嵌入的ARMS控制台的应用列表、应用详情、调用查询等页面。
-   可隐藏ARMS控制台的顶部菜单栏和左侧导航栏。具体操作，请参见[隐藏导航栏](#step_ejt_0s8_cjt)。
-   可通过访问控制RAM控制操作权限，例如将完整权限改为只读权限。具体操作，请参见[添加权限](#section_qcc_ejh_ix5)。

## 示例代码

如需快速体验将将ARMS页面嵌入自建Web应用的效果，您可以下载并使用[示例代码](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/demo/ARMS/Demo/embedPage.zip)。

## 访问流程

外部系统访问ARMS的流程如下图所示。

![access_flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54445.png)

## 步骤一：创建RAM用户并添加权限

使用阿里云账号创建RAM用户并为其添加调用STS服务扮演RAM角色的权限。

1.  登录[RAM控制台](http://ram.console.aliyun.com)。

2.  在左侧导航栏，选择**人员管理** \> **用户**。

3.  在用户页面，单击**创建用户**。

4.  在创建用户页面的**用户账号信息**区域，输入**登录名称**和**显示名称**，在**访问方式**区域，选中**编程访问**，然后单击**确定**。

    **说明：** RAM会自动为RAM用户创建AccessKey（API访问密钥）。出于安全考虑，RAM控制台只提供一次查看或下载AccessKeySecret的机会，即创建AccessKey时，因此请务必将AccessKeySecret记录到安全的地方。

5.  在手机验证对话框，单击**获取验证码**，输入收到的手机验证码，然后单击**确定**。

6.  在用户页面，找到创建好的用户，单击**操作**列的**添加权限**。

7.  在**添加权限**面板的**选择权限**区域，通过关键字搜索需要添加的权限策略AliyunSTSAssumeRoleAccess，并单击权限策略将其添加至右侧的**已选择**列表，然后单击**确定**。

    ![Add Permission For User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54441.png)

8.  在**添加权限**的**授权结果**页面，查看授权信息摘要，然后单击**完成**。


## 步骤二：创建RAM角色并添加权限

创建RAM角色并为其添加访问控制台的权限。RAM用户将会扮演该RAM角色访问控制台。

1.  登录[RAM控制台](http://ram.console.aliyun.com)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  在RAM角色管理页面，单击**创建RAM角色**。

4.  在**创建RAM角色**面板，执行以下操作：

    1.  在**选择类型**页面的**当前可信实体类型**区域，选择**阿里云账号**，然后单击**下一步**。

    2.  在**配置角色**页面的**角色名称**文本框，输入RAM角色名称，然后单击**完成**。

    3.  在**创建完成**页面，单击**为角色授权**。

5.  在**添加权限**面板的**选择权限**区域，搜索需要添加的权限策略，单击权限策略将其添加至右侧的**已选择**列表，然后单击**确定**。

    您可以根据需要为RAM角色赋予以下ARMS权限：

    -   AliyunARMSFullAccess：ARMS的完整权限。
    -   AliyunARMSReadOnlyAccess：ARMS的只读权限。
6.  在**添加权限**的**授权结果**页面，查看授权信息摘要，然后单击**完成**。


## 步骤三：获取临时AccessKey和Token

登录自建Web，然后在Web服务端调用STS的AssumeRole接口获取临时AccessKey和Token，即临时身份。AssumeRole接口详情，请参见[AssumeRole](/cn.zh-CN/API参考/API 参考（STS）/操作接口/AssumeRole.md)。

您可以选择以下方式调用AssumeRole接口：

-   通过[OpenAPI](https://api.aliyun.com/#/?product=Sts&api=AssumeRole)调用。
-   通过[Java SDK](/cn.zh-CN/SDK参考/SDK参考（RAM）/Java示例.md)调用。

本文以通过Java SDK调用为例。

您在使用Java SDK时需要注意填写以下参数：

```
String accessKey = "<accessKeyId>"; //RAM用户的AccessKeyId。
String accessSecret = "<accessKeySecret>"; //RAM用户的AccessKeySecret。
String roleArn = "<roleArn>"; //RAM角色的标识ARN。
```

RAM用户的AccessKeyId和AccessKeySecret为创建RAM用户时获取。

获取RAM角色的roleArn的操作步骤如下：

1.  登录[RAM控制台](http://ram.console.aliyun.com)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  在RAM角色管理页面下方的RAM角色列表，单击目标RAM角色名称。

4.  在RAM角色详情页面的**基本信息**区域，复制**ARN**信息。

    ![Example ARN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0012768951/p54443.png)


## 步骤四：获取登录Token

通过STS的AssumeRole接口获取临时AccessKey和Token后，调用登录服务接口获取登录Token。

**说明：** STS返回的安全Token中可能包含特殊字符，请对特殊字符进行URL编码后再输入。

请求样例：

```
http://signin.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<STS返回的临时AccessKeyId>
    &AccessKeySecret=<STS返回的临时AccessKeySecret>
    &SecurityToken=<STS返回的安全Token>
    &TicketType=mini
```

## 步骤五：生成免登录链接

利用获取到的登录Token与待嵌入的ARMS控制台页面链接生成免登录访问链接，以最终实现在自建Web中免登录访问ARMS控制台页面的目的。

**说明：** 由于Token有效期为3小时，建议在自建Web应用中将链接设置为每次请求时生成新登录Token。

1.  在ARMS控制台获取待嵌入的控制台页面的URL链接。

    例如杭州地域的应用列表页面的URL链接为：

    ```
    https://arms.console.aliyun.com/apm?iframeMode=true&demo=1&pid=ac346dab-419d-48f5-b06a-e1c331c5c93e&regionId=cn-shanghai#/ac346dab-419d-48f5-b06a-e1c331c5c93e/home
    ```

    **说明：**

    -   URL链接必须为ARMS应用监控的控制台地址，暂不支持ARMS前端监控的控制台地址。
    -   在URL链接的search部分添加`iframeMode=true`设置，可以隐藏ARMS控制台原有的顶部菜单栏和左侧导航栏。
2.  利用登录Token与ARMS控制台页面链接生成免登录访问链接。

    请求样例：

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<登录失效跳转的地址，一般配置为自建Web配置302跳转的URL>
        &Destination=<ARMS控制台页面链接>
        &SigninToken=<获取到的登录Token>
    ```


