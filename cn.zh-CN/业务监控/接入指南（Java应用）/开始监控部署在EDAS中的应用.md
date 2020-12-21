# 开始监控部署在EDAS中的应用

ARMS业务监控以代码无侵入的方式，可视化定义业务请求，并为您提供贴合业务的丰富性能指标与诊断能力。在使用业务监控之前，您需要先为您的EDAS应用完成安装探针或升级探针这一准备工作。

## 限制条件

-   业务监控仅支持监控Java应用。
-   只有2.6.2+版本的应用探针支持ARMS业务监控功能。

## 操作流程

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p103004.png)

**说明：** 扫描以下二维码图片加入钉钉答疑群。

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7067197951/p92785.png)

## 为EDAS中的Java应用安装探针

如果您是初次使用业务监控，并且未使用过应用监控的新用户，则按照应用监控的文档说明安装最新版本的探针，详情请参见[为部署在EDAS中的应用接入ARMS](/cn.zh-CN/应用监控/开始监控 Java 应用/为部署在EDAS中的应用接入ARMS.md)。

## 为EDAS中在ECS集群创建的Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本。如果是为EDAS中在ECS集群创建的Java应用升级探针，则按照以下步骤升级：

1.  登录[EDAS控制台](https://edas.console.aliyun.com)。

2.  在左侧导航栏中选择**应用管理** \> **应用列表**，单击要开启ARMS业务监控的应用名称。

    进入应用详情页面。

3.  在左侧导航栏中单击**基本信息**，在基本信息页面的实例部署信息页签右上角，单击**部署应用**，对应用进行部署发布，详情请参见[t1838948.md\#section\_d2h\_972\_4zb]()。

    ![tab_business_deployment_detail](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2067197951/p88780.png)

    部署发布完成后，即完成应用探针的自动升级。

4.  您可以连接并登录ECS实例，详情请参见[连接方式概述ECS远程连接操作指南](/cn.zh-CN/实例/连接实例/连接方式概述.md)。执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    版本号以2.6.2开头，则表示应用探针版本已成功升级至2.6.2+ 版本，此时您可以开始创建业务监控任务监控您的应用。


## 为EDAS中在K8s集群创建的Java应用升级探针

如果您是初次使用业务监控，并且已使用过应用监控的老用户，则在使用业务监控前，需将应用探针版本升级至2.6.2+版本。如果是为EDAS中在K8s集群创建的应用升级探针时，需要注意部署该应用的K8s集群导入EDAS的时间，2019年12月之前与之后的K8s集群应用升级操作有所不同：

1.  登录[EDAS控制台](https://edas.console.aliyun.com)。

2.  在左侧导航栏选择**资源管理** \> **集群**，在容器服务K8s集群页签，查看**创建时间**列的创建时间：

    -   如果创建时间在2019年12月之前，则需要先升级arms-pilot组件后才能升级探针，请执行[步骤](#step_b44_68o_1pf)&nbsp;[3](#step_b44_68o_1pf)。
    -   如果创建时间在2019年12月之后包括2019年12月，则直接执行[步骤](#step_5kr_tre_5pi)&nbsp;[6](#step_5kr_tre_5pi)。
3.  在容器服务K8s集群页签，单击**集群ID/ 名称**列的集群ID进入集群详情页面，复制**集群信息**区域的**csClusterId**字段。

4.  登录[容器服务管理控制台](https://cs.console.aliyun.com)，在集群列表页面，从**名称**列表选择**ID**，并在右边的输入框中输入上一步复制的**csClusterId**字段，自动搜索到对应的k8s集群后，单击右侧**操作**列的**控制台**。

    ![pg_business_ack_cluster_list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4067197951/p91060.png)

5.  在左侧导航栏从**命名空间**列表选择**arms-pilot**或**arms-pilot-system**，在概况页面的**容器组**区域，单击右下角的 图标，然后再单击**删除**，删除arms-pilot组件对应的容器组。

    ![sc_business_delete_pods](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4067197951/p91078.png)



    删除容器组后，会自动创建新的容器组。

6.  登录[EDAS控制台](https://edas.console.aliyun.com)，在左侧导航栏中选择**应用管理** \> **应用列表**，单击要开启ARMS业务监控的应用名称。

7.  在应用总览页面，单击右上角的**部署**或**部署历史版本**对应用进行部署发布，详情请参见[分批发布（K8s集群）]()或[金丝雀发布（K8s集群）]()。

    ![tab_business_deployment_detail_k8s](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2067197951/p91082.png)

    部署发布完成后，即完成应用探针的自动升级。

8.  在应用总览页面的**Pod信息总览**区域，单击**终端**后，执行`cat /home/admin/.opt/ArmsAgent/version`命令，查看应用探针的版本号。

    ![tab_business_deployment_detail_k8s_pod](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3067197951/p91084.png)

    若版本号以2.6.2开头，则表示应用探针版本已成功升级至2.6.2+ 版本，此时您可以创建业务监控任务监控您的应用。


**相关文档**  


[为部署在EDAS中的应用接入ARMS](/cn.zh-CN/应用监控/开始监控 Java 应用/为部署在EDAS中的应用接入ARMS.md)

