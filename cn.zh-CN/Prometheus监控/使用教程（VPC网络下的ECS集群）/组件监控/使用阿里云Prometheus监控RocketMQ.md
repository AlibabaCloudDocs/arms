# 使用阿里云Prometheus监控RocketMQ

阿里云Prometheus监控提供一键安装配置RocketMQ类型的组件，并提供开箱即用的专属监控大盘。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击Prometheus示例实例名称。

4.  在左侧导航栏单击**组件监控**。


## 添加RocketMQ类型的组件

1.  在组件监控页面，单击右上角的**添加组件监控**。

2.  在组件列表对话框右中单击RocketMQ组件图标。

3.  在RocketMQ组件配置对话框的**配置**页签输入各项参数。

    ![RocketMQ组件监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5386416261/p293829.png)

    |参数|描述|
    |--|--|
    |**组件名称**|组件的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
**说明：** 默认名称由组件类型及数字后缀组成。 |
    |**RocketMQ地址**|RocketMQ的连接地址。格式为：连接地址:端口号，多个地址之间使用半角逗号（,）分隔。**说明：** 支持部署在容器服务Kubernetes版的RocketMQ地址联想。 |
    |**用户名**|RocketMQ的AccessKey。|
    |**密码**|RocketMQ的SecretKey。|

4.  在RocketMQ组件配置对话框的**指标**页签查看监控指标。

5.  配置完成后，单击**确定**。

6.  在组件监控页面，单击**大盘**列的大盘链接，查看Prometheus监控大盘。

    ![RocketMQ-Exporter接入](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5834666161/p254827.png)


## 相关操作

在组件监控页面，可对已添加的组件执行以下操作：

-   单击**操作**列的**删除**，可删除已添加的组件。
-   单击**操作**列的**日志**，可查看组件的运行日志。
-   单击**操作**列的**详情**，可查看组件的详情，包括组件的环境变量和描述信息。

