# 将链路追踪控制台页面嵌入自建Web应用

如需在自建Web应用中免登录查看链路追踪控制台的页面，您可将链路追踪控制台嵌入自建Web应用，以此避免系统间的来回切换。

## 教程概述

**预期结果**

参照本教程的方法进行实际操作后将实现以下效果：

-   可登录您的自有系统并浏览嵌入的应用列表、应用详情、调用查询等页面。
-   可隐藏链路追踪页面的顶部导航栏和左侧导航栏。
-   可通过访问控制RAM系统控制操作权限，例如将完整权限改为只读权限等。

**访问流程**

使用本教程所述方法访问链路追踪页面的流程如图所示。

![Tracing Analysis Embedding Digram](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5192607951/p53905.png)

## 准备工作：创建RAM用户并添加权限

首先使用阿里云账号创建RAM用户并为其添加调用STS服务扮演RAM角色的权限。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中选择**人员管理** \> **用户**，并在用户页面上单击**新建用户**。

2.  在新建用户页面的**用户账号信息**区域框中，输入**登录名称**和**显示名称**。在**访问方式**区域框中，勾选**编程访问**，并单击**确认**。

    ![Create RAM User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9646888161/p53906.png)

    **说明：** RAM会自动为RAM用户创建AccessKey（API访问密钥）。出于安全考虑，RAM控制台只提供一次查看或下载AccessKeySecret的机会，即创建AccessKey时，因此请务必将AccessKeySecret记录到安全的地方。

3.  在手机验证对话框中单击**获取验证码**，并输入收到的手机验证码，然后单击**确定**。 创建的RAM用户显示在用户页面上，但此时没有任何权限。

4.  在用户页面上找到创建好的用户，单击**操作**列中的**添加权限**。

5.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略AliyunSTSAssumeRoleAccess，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

    ![Add Permission for User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9646888161/p53907.png)

6.  在**添加权限**面板，查看授权结果，并单击**完成**。


## 准备工作：创建RAM角色并添加权限

接下来创建RAM角色并为其添加访问链路追踪控制台的权限。上一步创建的RAM用户将会扮演该RAM角色访问链路追踪控制台。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中单击**RAM角色管理**，并在RAM角色管理页面上单击**新建RAM角色**。

2.  在**新建RAM角色**面板中执行以下操作并单击**确定**。

    1.  在**选择类型**页面的**当前可信实体类型**区域框中选择**阿里云账号**，并单击**下一步**。

    2.  在**配置角色**页面的**角色名称**文本框内输入RAM角色名称，并单击**完成**。

    3.  在**创建完成**页面上单击**为角色授权**。

3.  在**添加权限**面板的**选择权限**区域框中，通过关键字搜索需要添加的权限策略，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

    ![Add Permission for Role](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9646888161/p53909.png)

    -   如需添加链路追踪的完整权限，则添加AliyunTracingAnalysisFullAccess。
    -   如需添加链路追踪的只读权限，则添加AliyunTracingAnalysisReadOnlyAccess。
4.  在**添加权限**面板，查看授权结果，并单击**完成**。


## 步骤一：获取临时AccessKey和Token

登录自建Web后，在Web服务端调用STS [AssumeRole](/cn.zh-CN/API参考/API 参考（STS）/操作接口/AssumeRole.md)接口获取临时AccessKey和Token，即临时身份。请选择一种方式调用该接口：

-   通过[OpenAPI开发者门户](https://next.api.aliyun.com/api/Sts/2015-04-01/AssumeRole)在线调用。
-   通过[Java示例](/cn.zh-CN/SDK参考/SDK参考（RAM）/Java示例.md)调用。

请注意，在[\[示例代码\]](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip)中，您首先需要将以下参数替换为真实的值。

```
String akId = "<accessKeyId>";
String ak = "<accessKeySecret>";
String roleArn = "<roleArn>";
```

其中，<accessKeyId\>和<accessKeySecret\>是准备工作中创建的RAM用户的AccessKeyId和AccessKeySecret。

![Example AccessKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6192607951/p53911.png)

<roleArn\>是准备工作中创建的RAM角色的标识ARN，可在RAM控制台的RAM角色基本信息页面获取。

![Example ARN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9646888161/p53915.png)

## 步骤二：获取登录Token

在通过STS AssumeRole接口获取临时AccessKey和Token后，调用登录服务接口获取登录Token。

**说明：** STS返回的安全Token中可能包含特殊字符，请对特殊字符进行URL编码后再输入。

请求样例：

```
http://signin4service.aliyun.com/federation?Action=GetSigninToken
    &AccessKeyId=<STS返回的临时AccessKeyId>
    &AccessKeySecret=<STS返回的临时AccessKeySecret>
    &SecurityToken=<STS返回的安全Token>
    &TicketType=mini
```

## 步骤三：生成免登录链接

利用获取到的登录Token与待嵌入的链路追踪控制台页面链接生成免登录访问链接，以最终实现在自建Web中免登录访问链路追踪控制台页面的目的。

**说明：** 由于Token有效期为3小时，建议在自建Web应用中将链接设置为每次请求时生成新登录Token，通过302请求返回进行跳转。

1.  在链路追踪控制台获取待嵌入的控制台页面链接。例如杭州地域的应用列表页面的链接为：

    ```
    https://tracing-analysis.console.aliyun.com/?hideTopbar=true&hideSidebar=true#/appList/cn-hangzhou
    ```

    **说明：** 将hideTopbar设为true表示隐藏顶部导航栏，将hideSidebar设为true表示隐藏左侧导航栏。

2.  利用步骤二中获取到的登录Token与链路追踪控制台页面链接生成免登录访问链接。 请求样例：

    ```
    http://signin.aliyun.com/federation?Action=Login
        &LoginUrl=<登录失效跳转的地址，一般配置为自建Web配置302跳转的URL>
        &Destination=<链路追踪控制台页面链接>
        &SigninToken=<获取到的登录Token>
    ```


登录自建Web应用后，可见嵌入的链路追踪控制台页面效果如下图所示：

![Example Result of Embedding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6192607951/p53916.png)

本教程的示例代码基于Java SDK，以嵌入链路追踪控制台的应用列表为例。

[获取示例代码](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/tools/embedPage.zip)

