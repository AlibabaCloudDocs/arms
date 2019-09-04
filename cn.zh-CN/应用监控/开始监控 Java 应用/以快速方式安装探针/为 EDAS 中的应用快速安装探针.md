# 为 EDAS 中的应用快速安装探针 {#concept_65995_zh .concept}

借助 ARMS 应用监控，您可以对 EDAS 应用进行应用拓扑、接口调用、异常事务和慢事务监控、SQL 分析等监控。ARMS 与 EDAS 进行了功能集成，通过在 EDAS 控制台简单操作即可将 EDAS 应用快速接入 ARMS 应用监控。

## 在 EDAS 产品的组件中心开通 ARMS {#section_hdc_5pp_32b .section}

1.  登录 [EDAS 控制台](https://edas.console.aliyun.com/#/home)，在左侧导航栏中选择**组件中心** \> **组件概览**。
2.  在组件概览页面顶部的**分类**区域单击**微服务**，然后单击**应用监控** 右侧的**立即开通**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498443112_zh-CN.png)

3.  在**安全授权提示**对话框中单击**确定**，即可开通 ARMS 应用实时监控服务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498443113_zh-CN.png)


## 在 EDAS 中开启 ARMS 应用监控 {#section_rjc_5pp_32b .section}

1.  登录 [EDAS 控制台](https://edas.console.aliyun.com/#/home)，在左侧导航栏中选择**应用管理** \> **应用列表**，单击要开启 ARMS 应用监控的应用名称，进入应用详情页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498443114_zh-CN.png)

2.  在应用详情页面左侧导航栏中选择**应用监控** \> **高级监控**，单击**开启 ARMS 应用监控**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498543115_zh-CN.png)

3.  在提示对话框中单击**确认**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498543116_zh-CN.png)

4.  在提示对话框中单击**前去重启应用**，令 ARMS 应用监控生效。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498543117_zh-CN.png)


## 在 ARMS 中查看应用 {#section_hqc_5pp_32b .section}

成功开启 ARMS 应用监控并且重启应用后，单击**跳转至 ARMS 应用监控**，可跳转到 ARMS 应用列表页。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152234/156756498543118_zh-CN.png)

在应用列表页面输入应用名称即可查看应用详情。更多 ARMS 应用监控的使用方法请参见[应用监控概述](intl.zh-CN/应用监控/应用监控概述.md#)。

