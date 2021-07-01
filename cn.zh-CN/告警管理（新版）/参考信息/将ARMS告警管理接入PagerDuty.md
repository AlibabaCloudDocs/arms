# 将ARMS告警管理接入PagerDuty

PagerDuty是一款为企业IT部门提供事件响应的软件。您可以将ARMS告警管理接入PagerDuty从而触发自动事件或追踪服务变化。

PagerDuty是一款为企业IT部门提供事件响应的软件。当服务出现问题时，PagerDuty支持以电话、短信、邮件等方式通知企业IT部门。关于PagerDuty的更多信息，请参见[PagerDuty官网](https://www.pagerduty.com/company/)。

## 步骤一：注册PagerDuty账号

您可以在PagerDuty官网注册14天免费试用的PagerDuty账号。操作步骤如下：

1.  打开[PagerDuty注册页面](https://www.pagerduty.com/sign-up/)。

2.  在**Try PagerDuty**配置向导区域，执行以下操作：

    1.  输入邮箱，然后单击**GET STARTED!**。

    2.  输入姓名，然后单击**NEXT STEP**。

    3.  输入密码，然后单击**NEXT STEP**。

    4.  输入子域名，选中服务协议，然后单击**CREATE ACCOUNT**。

    注册完成后跳转到PagerDuty欢迎页面。

    ![Welcome](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2201085161/p249199.png)


## 步骤二：创建服务

在PagerDuty控制台为ARMS告警管理创建对应的服务。操作步骤如下：

1.  登录[PagerDuty控制台](https://app.pagerduty.com/)。

2.  在顶部菜单栏，选择**Services** \> **Service Directory**。

3.  在**Service Directory**页面，单击**+ New Service**。

4.  在**Create a Service**页面，执行以下操作：

    1.  输入服务名称，然后单击**NEXT**。

    2.  选择**Generate a new Escalation Policy**，然后单击**NEXT**。

    3.  选择**Intelligent**，然后单击**NEXT**。

    4.  根据需求选择**Events API v1**或**Events API V2**，然后单击**Create Service**。

        **说明：** **Events API v1**和**Events API V2**均可以将ARMS告警管理连接到PagerDuty，但**Events API V2**提供了一个直接接口来设置PagerDuty告警中的[PD-CEF](https://support.pagerduty.com/docs/pd-cef)字段，使ARMS告警管理更容易在PagerDuty中生成丰富的告警数据，实现分类、过滤和操作。更多信息，请参见[Events API](https://developer.pagerduty.com/docs/get-started/getting-started/#events-api)。

5.  在Integrations区域复制并保存**Events API v1**的**Integration Key**和**Integration URL**，**Events API V2**的**Integration Key**和**Integration URL \(Alert Events\)**。

    ![Integrations的Key和URL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1521624261/p285500.png)


## 步骤三：创建Webhook



根据需要选择为**Events API v1**或**Events API V2**创建Webhook，通过Webhook将告警发送至PagerDuty中。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**告警管理** \> **联系人**。

3.  在**联系人**页签，单击**新建Webhook**。

4.  在**创建Webhook**对话框，设置以下参数，然后单击**确认**。

    1.  输入Webhook名称。

    2.  设置**Post**为**Events API v1**的**Integration URL**。

    3.  使用以下格式在Body的文本框中输入**Integration Key**。

        ```
        integration_key=********4463
        ```

5.  单击**测试**。

    当返回信息中出现`status=success`时表示配置成功。

    ![PagerDuty配置Webhook](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2957234261/p285562.png)

6.  单击**创建**。


1.  在**联系人**页签，单击**新建Webhook**。

2.  在**创建Webhook**对话框，设置以下参数，然后单击**确认**。

    1.  输入Webhook名称。

    2.  设置**Post**为**Events API V2**的**Integration URL \(Alert Events\)**。

    3.  使用以下格式在Body的文本框中输入**Integration Key**。

        ```
        integration_key=********4463
        ```

3.  单击**测试**。

    当返回信息中出现`status=success`时表示配置成功。

4.  单击**创建**。


创建完成后可以在联系人页签查看创建的PagerDuty联系人。

![PagerDuty联系人](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2957234261/p285819.png)

## 步骤四：创建通知策略

将创建的Webhook设置为告警通知对象。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**告警管理** \> **通知策略**。

3.  在**通知策略**页面的通知策略列表区域，单击**+新增策略**。

4.  在**通知策略**页面右侧，输入通知策略的名称，在**事件处理**区域，选择**处理方式**为**生成告警**，在**当告警生成时**区域，选择**通知人**为创建的Webhook，选择**通知方式**为**Webhook**。

    其他参数的设置，请参见[通知策略](/cn.zh-CN/告警管理（新版）/控制台操作/通知策略.md)。

5.  在页面右上角，单击确认图标。


