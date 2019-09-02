# SDK 数据源概述 {#concept_52320_zh .concept}

ARMS 集成了阿里云日志服务的 Logstash SDK，您可以通过程序 SDK 集成直接推送数据到 ARMS。

接入 SDK 数据源主要分为两个步骤：

1.  创建 SDK 数据源。
2.  通过 SDK 写入数据到创建好的数据源。

## 创建 SDK 数据源 {#section_in3_5qs_gfb .section}

1.  在 ARMS 控制台左侧导航栏中选择**自定义监控数据源管理** \> **SDK 数据源**。
2.  在实例列表页面上，单击右上角的**创建 SDK 数据源**，并在提示对话框中单击**确定创建**。

    **说明：** 一个地域中至多可以创建 20 个 SDK 数据源。

    创建的 SDK 数据源显示在实例列表页面的列表中。


创建完毕后，在为自定义监控配置数据源（参见[配置数据源](intl.zh-CN/自定义监控/创建监控任务/配置数据源.md#)）时，只需在**日志源类型**下拉列表中选择 **SDK 数据源**，即可在**选择日志源**下拉列表中看到创建好的 SDK 数据源。

## 通过 SDK 将数据写入创建好的数据源 {#section_me5_ghb_h6m .section}

通过 ARMS SDK，您可以将数据写入创建的数据源。目前支持 Java 和 Python。ARMS 采用了日志服务的 API，具体使用方法参见日志服务 SDK 文档“[概述](../../../../intl.zh-CN/SDK 参考/基本介绍/概述.md#)”。除了填写 endpoint、project、logstore、AK、SK 方法不同以外，其他方法类似。

-   AK、SK：在实例列表页面上，单击**操作**栏中的**获取 AccessKeys**，即可在获取 AccessKeys对话框中找到该信息。

-   LogStore、Project：在实例列表页面的表格中。

-   Endpoint：见下表。

    |区域|endpoint|
    |--|--------|
    |北京|cn-beijing.log.aliyuncs.com|
    |青岛|cn-qingdao.log.aliyuncs.com|
    |上海|cn-shanghai.log.aliyuncs.com|
    |杭州|cn-hangzhou.log.aliyuncs.com|
    |深圳|cn-shenzhen.log.aliyuncs.com|


