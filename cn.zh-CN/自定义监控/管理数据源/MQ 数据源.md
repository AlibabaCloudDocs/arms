# MQ 数据源 {#concept_zvk_1gh_jhb .concept}

如果您已开通消息队列 MQ，ARMS 可直接统计 MQ 消息的内容。关于利用 MQ 数据源进行监控的案例，请参考[车联网实时监控方案](../intl.zh-CN/产品简介/应用场景/车联网实时监控方案.md#)。

## 前提条件 {#section_oj2_h3d_dhb .section}

-   您已开通[阿里云消息队列 RocketMQ](https://www.alibabacloud.com/product/mq)，且已创建 Topic。

## 操作步骤 {#section_i4z_g3d_dhb .section}

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。
2.  在控制台左侧导航栏中选择**自定义监控数据源管理** \> **MQ 数据源**。如果此前未授权 ARMS 读取 MQ 数据，则 ARMS 会给出提示信息。

3.  在提示对话框中单击**确定授权**，然后在确认对话框中单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152300/156756317543715_zh-CN.png)

4.  在 MQ 数据源页面右上角单击**刷新**。您在该地域所拥有的 MQ Topic 将显示在该页面上。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152300/156756317543716_zh-CN.png)


## 后续操作 {#section_swr_1gd_dhb .section}

MQ 数据源刷新成功后，您可以前往**自定义监控** \> **监控任务管理**页面创建自定义监控任务。在自定义监控任务的数据源配置页面上，当选择 **MQ 数据源**作为**日志源类型**并选择 **Region** 后，您在该 Region（地域）的 MQ Topic 将显示在 **Topic** 下拉列表中。

## 更多信息 {#section_fwh_lgd_dhb .section}

-   [配置数据源](intl.zh-CN/自定义监控/创建监控任务/配置数据源.md#)

