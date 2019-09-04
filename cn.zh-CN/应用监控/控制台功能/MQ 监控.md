# MQ 监控 {#concept_98847_zh .concept}

ARMS 应用监控的 MQ 监控可展示[消息队列 RocketMQ](https://help.aliyun.com/document_detail/29532.html?spm=a2c4g.11174283.4.1.11ca449cquWQNe) Topic 发布和订阅消息的情况。

## 功能入口 {#section_ewd_cb4_yfb .section}

请按照以下步骤进入 ARMS 应用监控的 MQ 监控页面。

1.  登录[ARMS 控制台](https://arms.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表** 。
2.  在应用列表页面，单击目标应用的名称。

3.  在左侧导航栏中单击 **MQ 监控**。

4.  在页面右侧单击查询结果的链接。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152245/156756488843141_zh-CN.png)


完成以上步骤后，即可进入 MQ 监控页面的概览页签。

## 功能介绍 {#section_w2h_cb4_yfb .section}

MQ 监控页面具备以下功能：

-   在拓扑图中展示应用与 MQ 数据源之间的消息发布和订阅关系。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152245/156756488943142_zh-CN.png)

-   展示消息发布的统计数据，包括请求数、响应时间和错误数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152245/156756488943143_zh-CN.png)

-   展示消息订阅的统计数据，包括消息请求数、响应时间和错误数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152245/156756488943144_zh-CN.png)

-   提供关于消息发布和订阅的接口快照，您可以通过 TraceId 链接查看完整调用链以及诊断问题原因。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152245/156756488943146_zh-CN.png)


## 可用操作 {#section_smh_cb4_yfb .section}

-   在页面右上角的时间选择框内选择需要查看统计数据的起止时间。
-   单击**发布端统计**和**订阅端统计**页签，查看消息发布和订阅的统计数据。
-   单击**接口快照**页签，查看关于消息发布和订阅的接口快照，必要时可通过 TraceId 链接查看完整调用链以及诊断问题原因。
-   单击**返回总览**，回到 MQ 监控页面。

