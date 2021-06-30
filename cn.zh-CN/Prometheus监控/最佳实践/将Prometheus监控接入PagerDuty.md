# 将Prometheus监控接入PagerDuty

PagerDuty是一款为企业IT部门提供事件响应的软件。您可以将Prometheus监控接入PagerDuty从而触发自动事件或追踪服务变化。

-   您的K8s集群已接入Prometheus监控。具体操作，请参见[容器服务Kubernetes版集群]()。
-   您已创建报警规则，且报警规则处于启用状态并被触发。具体操作，请参见[创建报警]()。

PagerDuty是一款为企业IT部门提供事件响应的软件。当服务出现问题时，PagerDuty支持以电话、短信、邮件等方式通知企业IT部门。关于PagerDuty的更多信息，请参见[PagerDuty官网](https://www.pagerduty.com/company/)。

## 操作流程

将Prometheus监控接入PagerDuty的操作流程如下图所示。

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1471085161/p249807.png)

## 步骤一：注册账号

注册14天免费试用的PagerDuty账号的操作步骤如下：

1.  打开[PagerDuty注册页面](https://www.pagerduty.com/sign-up/)。

2.  在**Try PagerDuty**配置向导区域，执行以下操作：

    1.  输入邮箱，然后单击**GET STARTED**。

    2.  输入姓名，然后单击**NEXT STEP**。

    3.  输入密码，然后单击**NEXT STEP**。

    4.  输入子域名，选中服务协议，然后单击**CREATE ACCOUNT**。

    注册完成后跳转到PagerDuty欢迎页面。

    ![Welcome](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2201085161/p249199.png)


## 步骤二：创建服务

在PagerDuty控制台为Promethues监控创建对应的服务的操作步骤如下：

1.  登录[PagerDuty控制台](https://app.pagerduty.com/)。

2.  在顶部菜单栏，选择**Services** \> **Service Directory**。

3.  在**Service Directory**页面，单击**New Service**。

4.  在**Add a Service**页面，输入服务名称，选择**Integration Type**为**Prometheus**，然后单击**Add Service**。

    **说明：** 您可以根据业务需求设置Service的其他参数。

    跳转的页面显示创建的服务的信息。

    ![service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2201085161/p249259.png)


## 步骤三：获取Integration Key

获取用于将Prometheus监控接入PagerDuty的Integration Key的操作步骤如下：

1.  在创建的服务的页面下方，单击**Integrations**页签。

2.  在**Integrations**区域，找到Prometheus服务，在其右侧**Integration Key**列，单击复制图标将Integration Key复制到剪贴板。

    ![integration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2201085161/p249295.png)


## 步骤四：创建联系人

使用Integration Key创建联系人的操作步骤如下：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**报警管理** \> **联系人管理**。

3.  在**联系人管理**页面，单击**新建联系人**。

4.  在**新建联系人**对话框，输入姓名，将**钉钉机器人**设置为获取的Integration Key，然后单击**确认**。

    ![contact](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3201085161/p249309.png)


## 步骤五：创建通知策略

为联系人创建通知策略的操作步骤如下：

1.  登录[Prometheus控制台](https://prometheus.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**通知策略**。

3.  在**通知策略**页面的**通知策略列表**区域，单击**新增策略**。

4.  在**通知策略**页面右侧，输入通知策略的名称，在**事件处理**区域，选择**处理方式**为**生成告警**，在**当告警生成时**区域，选择**通知人**为创建的联系人，选择**通知方式**为**钉钉**，设置**通知时段**，然后在右上角，单击确认图标。

    ![通知策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3201085161/p249801.png)


## 步骤六：修改报警规则

将报警规则的通知策略修改为创建的通知策略的操作步骤如下：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后单击目标K8s集群的名称。

4.  在左侧导航栏，单击**报警配置**。

5.  在报警配置页面，找到目标报警规则，在其右侧**操作**列，单击**编辑**。

6.  在**编辑报警**面板的**通知策略**下拉列表，选择创建的通知策略，然后单击**确定**。


## 结果验证

您可以在PagerDuty控制台查看报警以验证是否成功接入。

1.  登录[PagerDuty控制台](https://app.pagerduty.com/)。

2.  在顶部菜单栏，选择**Incidents** \> **Alerts**。

    **Alerts on All Teams**页面显示触发的报警。

    ![Alerts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3201085161/p249804.png)

3.  如需查看Alert的详细信息，在**Summary**列，单击目标Alert的名称。


