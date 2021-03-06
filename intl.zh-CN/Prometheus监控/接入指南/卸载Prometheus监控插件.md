# 卸载Prometheus监控插件

如需停止对Kubernetes集群的Prometheus监控，请按照以下步骤卸载Prometheus监控插件。

## 操作步骤

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面左上角选择目标地域，单击**操作**列中的**卸载**，并在**确认**对话框中单击**确认**。

    卸载插件完毕后，**已安装大盘**列中的大盘将会消失。接下来需要前往容器服务管理控制台确认卸载是否成功。

4.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

5.  在左侧导航栏单击**集群**，然后单击需停止监控的集群名称。

    **说明：** 本文中关于容器服务管理控制台的步骤描述仅适用于新版控制台。如果您使用的是旧版控制台，请在左侧导航栏选择**集群** \> **集群**，然后在页面右上角单击**体验新版**。

6.  在左侧导航栏单击**发布**，并根据情况采取以下任一操作：

    -   如果**发布**页面没有`arms-prom-****`记录，则说明监控插件卸载成功，您无需采取任何操作。
    -   如果**发布**页面有`arms-prom-****`记录，请在其右侧的**操作**列中单击**删除**。

        ![ack_pg_release](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4616183161/p143010.png)


