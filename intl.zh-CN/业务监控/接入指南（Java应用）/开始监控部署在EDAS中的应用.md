# 开始监控部署在EDAS中的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的EDAS应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0784574161/p103004.png)

**说明：** 欢迎您使用钉钉扫描下方二维码或者搜索钉钉群号30004969加入钉钉群进行反馈。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1789717161/p92785.png)

## 为EDAS中的Java应用安装探针

如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针。具体操作，请参见[为部署在EDAS中的应用接入ARMS](/intl.zh-CN/应用监控/接入应用监控/开始监控Java应用/为部署在EDAS中的应用接入ARMS.md)。

## 为EDAS中在ECS集群创建的Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本。如果是为EDAS中在ECS集群创建的Java应用升级探针，则按照以下步骤升级：

1.  登录[EDAS控制台](https://edas-intl.console.aliyun.com)。

2.  在左侧导航栏，选择**应用管理** \> **应用列表**。

3.  在顶部菜单栏，选择地域。

4.  在**应用列表**页面，单击要开启业务监控的应用名称。

5.  在页面的右上角，单击**部署应用**，然后部署应用。

    如何部署应用，请参见[t1838948.md\#section\_d2h\_972\_4zb]()。

    部署完成后，应用探针自动升级。

6.  您可以连接并登录ECS实例，执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    如何连接并登录ECS实例，请参见[连接方式概述ECS远程连接操作指南](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

    版本号以2.6.2或以上开头，则表示应用探针版本已成功升级至2.6.2+版本，此时您可以开始创建业务监控任务监控您的应用。


## 为EDAS中在K8s集群创建的Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本。如果是为EDAS中在K8s集群创建的应用升级探针时，需要注意部署该应用的K8s集群导入EDAS的时间，2019年12月之前与之后的K8s集群应用升级操作有所不同：

1.  登录[EDAS控制台](https://edas-intl.console.aliyun.com)。

2.  在左侧导航栏，选择**资源管理** \> **容器服务K8s集群**。

3.  在顶部菜单栏，选择地域。

4.  在**容器服务K8s集群**页面，单击目标集群ID。

5.  在**集群详情**页面的**集群信息**区域，单击**查看详情**。

    -   如果**创建时间**为2019年12月1日之前，则需要先升级arms-pilot组件后才能升级探针，请从[步骤6](#step_b44_68o_1pf)开始执行。
    -   如果**创建时间**为2019年12月1日或之后，则无需升级arms-pilot组件就能升级探针，请从[步骤10](#step_w77_b7m_zrc)开始执行。
6.  登录[容器服务管理控制台](https://partners-intl.console.aliyun.com/#/cs)。

7.  在集群列表页面，单击目标集群名称。

8.  在左侧导航栏，选择**工作负载** \> **容器组**。

9.  从**容器组**页面的**命名空间**列表，选择**arms-pilot**，在arms-pilot组件对应的容器组右侧，单击**删除**。

    删除容器组后，会自动创建新的容器组。

10. 登录[EDAS控制台](https://edas-intl.console.aliyun.com)。

11. 在左侧导航栏，选择**应用管理** \> **应用列表**。

12. 在顶部菜单栏，选择地域。

13. 在**应用列表**页面，单击要开启业务监控的应用名称。

14. 在**应用总览**页面的右上角，选择**部署** \> **部署**，然后部署应用。

    如何部署应用，请参见[使用控制台分批发布应用（K8s）]()或[使用控制台金丝雀发布应用（K8s）]()。

    部署完成后，应用探针自动升级。

15. 在**应用总览**页面的**基本信息**区域的**运行状态**的右侧，单击运行中的Pod，在**应用配置详情**面板，找到目标容器组，在其右侧**操作列**，单击**终端**，在终端界面，执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    版本号以2.6.2或以上开头，则表示应用探针版本已成功升级至2.6.2+版本，此时您可以创建业务监控任务监控您的应用。


**相关文档**  


[为部署在EDAS中的应用接入ARMS](/intl.zh-CN/应用监控/接入应用监控/开始监控Java应用/为部署在EDAS中的应用接入ARMS.md)

