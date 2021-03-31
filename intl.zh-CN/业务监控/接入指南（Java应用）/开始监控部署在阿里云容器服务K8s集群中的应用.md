# 开始监控部署在阿里云容器服务K8s集群中的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的Java应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0784574161/p103004.png)

**说明：** 欢迎您使用钉钉扫描下方二维码或者搜索钉钉群号30004969加入钉钉群进行反馈。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1789717161/p92785.png)

## 为容器服务Kubernetes版Java应用安装探针

如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针。具体操作，请参见[为容器服务Kubernetes版Java应用安装探针](/intl.zh-CN/应用监控/接入应用监控/开始监控Java应用/为容器服务Kubernetes版Java应用安装探针.md)。

## 为容器服务Kubernetes版Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本：

1.  登录[容器服务管理控制台](https://partners-intl.console.aliyun.com/#/cs)。

2.  在左侧导航栏，单击**集群**。

3.  在**集群列表**，单击目标集群ID。

4.  在左侧导航栏，选择**应用** \> **Helm**。

    ![tab_business_helm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5874800161/p93070.png)

    -   如果arms-pilot组件的更新时间在2019年12月1日之前，则需要先升级arms-pilot组件后才能升级探针，请从[步骤5](#step_zth_q9r_1kt)开始执行。
    -   如果arms-pilot组件的更新时间在2019年12月1日或之后，则无需升级arms-pilot组件就能升级探针，请从[步骤7](#step_ud6_l2w_izu)开始执行。
5.  在左侧导航栏，单击**工作负载** \> **容器组**。

6.  从**容器组**页面的**命名空间**列表，选择**arms-pilot**，在arms-pilot组件对应的容器组右侧，单击**删除**。

    删除容器组后，会自动创建新的容器组。

7.  重启您的业务Pod。

    应用探针自动升级。

8.  在容器内执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    版本号以2.6.2或以上开头，则表示应用探针版本已成功升级至2.6.2+版本，此时您可以创建业务监控任务监控您的应用。


**相关文档**  


[准备工作概述](/intl.zh-CN/业务监控/接入指南（Java应用）/准备工作概述.md)

