# 开始使用 Prometheus 监控 {#concept_1062555 .concept}

对于部署在阿里云容器服务 Kubernetes 版中的 Kubernetes 集群，您可以在 ARMS 中为其一键安装 Prometheus 监控插件，此后即可通过 ARMS 预定义的仪表板监控主机和 Kubernetes 集群的众多性能指标。

## 前提条件 {#section_gg2_3tt_gkq .section}

-   [快速创建Kubernetes集群](../../../../../intl.zh-CN/快速入门/基础入门/快速创建Kubernetes集群.md#)：在阿里云容器服务 Kubernetes 版中创建 Kubernetes 集群。
-   [开通 ARMS](../intl.zh-CN/快速入门/开通 ARMS.md#)

## 安装 Prometheus 监控插件 {#section_cpd_cg9_vul .section}

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，并在页面左上角选择所需地域。
2.  在左侧导航栏中单击 **Prometheus 监控**。

    Prometheus 监控页面会列出您的阿里云账号下在阿里云容器服务 Kubernetes 版中的全部 Kubernetes 集群。

3.  在 Prometheus 监控页面上，单击**操作**列中的**安装**，并在提示对话框中单击**确认**。

    安装插件过程中，**操作**列将以进度条和百分比显示安装进度。

    安装插件完毕后，**已安装插件**列中将显示全部已安装的插件。


## 打开 Prometheus 监控仪表板 {#section_hg4_crq_33b .section}

1.  在左侧导航栏中单击 **Prometheus 监控**。

2.  在 Prometheus 监控页面上，单击**已安装插件**列中的链接，即可在浏览器新窗口中打开对应的监控仪表板。


## 卸载监控插件 {#section_vh2_dsq_33b .section}

如需停止对 Kubernetes 集群的 Prometheus 监控，请按照以下步骤卸载 Prometheus 监控插件。

1.  在左侧导航栏中单击 **Prometheus 监控**。

2.  在 Prometheus 监控页面上，单击**操作**列中的**卸载**，并在提示对话框中单击**确认**。

    卸载插件完毕后，**已安装插件**列中的插件将会消失。


## 后续步骤 {#section_bsg_qsq_33b .section}

[ZH-CN\_TP\_868729.md\#](intl.zh-CN/Prometheus 监控/查看 Prometheus 监控指标.md#)

## 更多信息 {#section_cdx_yj4_bbd .section}

[Prometheus 监控概述](intl.zh-CN/Prometheus 监控/Prometheus 监控概述.md#)

