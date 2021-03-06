# 将多个账号的ARMS告警集中到一个账号下处理

本文主要介绍如何通过ARMS告警管理的转发功能，将一个云账号的ARMS告警发送到另外一个云账号进行统一处理。

在ARMS中，资源是按照账号进行租户隔离的。用户在一个云账号中只能查看本账号的告警信息，无法处理跨账号的告警信息。但在运维部门（公司）同时使用多个云账号的场景下，运维人员则需要在每个云账号下单独处理该账号的告警，使得运维成本增加。

通过ARMS告警管理的转发功能，您可以将所有云账号的ARMS告警统一发送到一个云账号下进行处理。

本文的示例场景为：一个运维部门需要将B账号和C账号的ARMS告警事件上报到A账号进行统一管理。

**说明：** ARMS告警管理的转发功能仅支持转发ARMS产生的告警事件，不支持转发集成的其他告警源的告警事件。

## 步骤一：创建集成

在A账号下创建ARMS告警管理的集成，并获取集成密钥。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**告警管理** \> **集成**。

3.  在集成页面的支持集成区域单击**ARMS**。

4.  在添加集成配置向导页面，进行以下配置：

    1.  在基本信息向导页输入集成名称和描述，然后单击**下一步**。

    2.  在告警源配置向导页根据需求配置自动恢复告警事件的时间，然后单击**保存**。

        **说明：** 自动恢复告警事件：相同名称和等级的告警，在设置的时间内的多次上报会被合并为一条告警。当一条告警超过设置的时间后不再产生，则该告警状态自动变为已解决。

    配置完成后，在集成页面可以查看已创建的ARMS集成。

    ![ARMS集成-多账号告警汇集](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4667912261/p276864.png)

5.  在集成页面，单击ARMS集成的密钥，在集成详情页面复制集成密钥。


## 步骤二：上报告警

将B账号和C账号的ARMS中产生的告警上报至A账号的告警管理中。

1.  使用B账号和C账号分别登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**告警管理** \> **集成**。

3.  在集成页面的ARMS-DEFAULT集成右侧操作列，单击**转发告警**。

4.  在弹出的ARMS-DEFAULT转发告警对话框，输入A账号创建集成的密钥，然后单击**确认**。

    配置完成后，ARMS-DEFAULT集成右侧操作列变为**停止转发**。

    **说明：**

    单击**停止转发**，在弹出的对话框中单击**确认**，然后单击**保存**。可以停止将B账号或C账号的ARMS告警上报至A账号中。

    ![多账号ARMS告警汇集-上报完成](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4667912261/p276880.png)


**相关文档**  


[集成概述](/cn.zh-CN/告警管理（新版）/控制台操作/集成/集成概述.md)

