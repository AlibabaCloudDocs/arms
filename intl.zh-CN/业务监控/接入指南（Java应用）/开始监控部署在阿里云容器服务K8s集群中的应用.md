# 开始监控部署在阿里云容器服务K8s集群中的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的Java应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p103004.png)

**说明：** 扫描以下二维码图片加入钉钉答疑群。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p92785.png)

## 为容器服务Kubernetes版Java应用安装探针

如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[为容器服务Kubernetes版Java应用安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/为容器服务Kubernetes版Java应用安装探针.md)。

## 为容器服务Kubernetes版Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本：

1.  登录[容器服务管理控制台](https://partners-intl.console.aliyun.com/#/cs)，在左侧导航栏选择**应用** \> **发布**，在Helm页签查看ack-arms-pilot组件的更新时间。

    ![tab_business_helm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4067197951/p93070.png)

    -   如果更新时间在2019年12月之前，则需要先升级ack-arms-pilot组件后才能升级探针，请执行[步骤](#step_zth_q9r_1kt)[2](#step_zth_q9r_1kt)。
    -   如果创建时间在2019年12月之后包括2019年12月，则直接执行[步骤](#step_ud6_l2w_izu)[4](#step_ud6_l2w_izu)。
2.  在左侧导航栏选择**集群** \> **集群**，在集群列表页面上的目标集群右侧**操作**列，单击**控制台**。

    ![pg_business_ack_cluster_list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4067197951/p91060.png)

3.  在左侧导航栏从**命名空间**列表选择**arms-pilot**或**arms-pilot-system**，在概况页面的**容器组**区域，单击右下角的 图标，然后再单击**删除**，删除arms-pilot组件对应的容器组。

    ![sc_business_delete_pods](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4067197951/p91078.png)



    删除容器组后，会自动创建新的容器组。

4.  重启您的业务Pod。

    应用探针自动升级。

5.  在容器内执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    若版本号以2.6.2开头，则表示应用探针版本已成功升级至2.6.2+ 版本，此时您可以创建业务监控任务监控您的应用。


**相关文档**  


[准备工作概述]()

