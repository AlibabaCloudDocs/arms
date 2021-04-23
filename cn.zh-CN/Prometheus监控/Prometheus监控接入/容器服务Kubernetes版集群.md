# 容器服务Kubernetes版集群

本文说明如何将容器服务Kubernetes版集群接入Prometheus监控，从而使用预定义的大盘监控主机和Kubernetes集群的众多性能指标。

-   已创建容器服务Kubernetes版集群。具体操作，请参见[快速创建Kubernetes托管版集群](/cn.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)。
-   已开通ARMS。具体操作，请参见[开通和升级ARMS](/cn.zh-CN/快速入门/开通和升级ARMS.md)。

## 开启阿里云Prometheus监控

您可以通过以下三种方式开启阿里云Prometheus监控：

**通过配置集群参数开启Prometheus监控。**

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在控制台左侧导航栏中，单击**集群**。

3.  在集群列表页面中，单击页面右上角的**创建集群**。

4.  选择目标集群模板，然后配置创建集群参数。在**组件配置**页面，选中**使用Prometheus监控服务**。

    ![组件配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5816545161/p248500.png)

    有关创建集群的具体步骤，请参见[创建Kubernetes托管版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes托管版集群.md)。

    **说明：** 在创建集群时，系统默认选中**使用Prometheus监控服务**。

    集群创建完成后，系统将自动配置阿里云Prometheus监控服务。


**通过ACK控制台Prometheus监控开启Prometheus监控。**

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在控制台左侧导航栏中，单击**集群**。

3.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。

4.  在集群管理左侧导航栏中，选择**运维管理** \> **Prometheus监控**。

5.  在**Prometheus监控**页面中间，单击**开始安装**。


**通过ACK控制台应用目录开启阿里云Prometheus监控。**

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在控制台左侧导航栏中，选择**市场** \> **应用目录**。

3.  在应用目录页面的**阿里云应用**页签中，搜索并单击**ack-arms-prometheus**。

4.  在应用目录 - ack-arms-prometheus右侧的**创建**区域中，选择目标集群，然后单击**创建**。

    **说明：** **命名空间**和**发布名称**默认为**arms-prom**。


**执行结果**

安装完成后会自动跳转到应用arms-prom页面，可查看应用信息。

![arm-prom](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5816545161/p248613.png)

## 打开Grafana大盘

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后在**已安装大盘**列，单击需要查看的大盘。


## 卸载监控插件

如需停止对Kubernetes集群的Prometheus监控，请按照以下步骤卸载Prometheus监控插件。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，找到要卸载的K8s集群，然后在其右侧**操作**列，单击**卸载**。

4.  在**确认**对话框，单击**确认**。

    卸载插件完毕后，**已安装大盘**列中的大盘消失。

5.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

6.  在左侧导航栏单击**集群**，然后单击需停止监控的集群名称。

7.  在左侧导航栏选择**应用** \> **Helm**，并根据情况采取以下任一操作：

    -   如果**Helm**页面没有`arms-prom-****`记录，则说明监控插件卸载成功，您无需采取任何操作。
    -   如果**Helm**页面有`arms-prom-****`记录，请在其右侧的**操作**列中单击**删除**。

        ![ack_pg_release](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4616183161/p143010.png)


