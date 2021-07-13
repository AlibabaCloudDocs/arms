# 新建Prometheus实例（ECS集群）

本文说明如何将VPC网络的ECS集群接入Prometheus监控，并创建大盘监控ECS集群的众多性能指标。

-   已开通ARMS。具体操作，请参见[开通和升级ARMS](/cn.zh-CN/快速入门/开通和升级ARMS.md)。
-   已创建VPC网络和ECS实例。具体操作，请参见[搭建IPv4专有网络](/cn.zh-CN/快速入门/搭建IPv4专有网络.md)。

## 开启阿里云Prometheus监控

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后单击**新建Prometheus实例**。

4.  在**新建Prometheus实例**页面，单击**ECS集群（VPC）**区域。

    在接入 ECS集群\(VPC\)面板显示当前地域下的所有VPC列表。

5.  在接入 ECS集群\(VPC\)面板的目标VPC右侧操作列，单击**安装**。

6.  在安装Prometheus应用对话框中，输入VPC名称，选择交换机和安全组，然后单击**确定**。

    ![VPC接入Prometheus](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3226275261/p290536.png)

    -   VPC名：自定义VPC显示名称。
    -   交换机：选择需要监控的ECS实例所在的交换机。
    -   安全组：选择需要监控的ECS实例所在的安全组。
    安装成功后，对应VPC右侧状态列显示安装成功。

    ![vpc安装成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6532475261/p292834.png)


## 创建大盘

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域。

    **Prometheus监控**页面显示了所有接入Prometheus监控的集群，其中，环境类型为vpc-prometheus的即为VPC网络下的ECS集群。

    ![VPC集群大盘](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3226275261/p290547.png)

4.  单击ECS集群名称。

5.  在大盘列表页面右上角单击**创建大盘**。

6.  根据需求在Grafana控制台创建大盘。具体操作，请参见[Grafana文档](https://grafana.com/docs/grafana/latest/dashboards/?pg=docs)。


## 卸载监控插件

如需停止ECS集群的Prometheus监控，请按照以下步骤卸载Prometheus监控插件。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**Prometheus监控**。

3.  在**Prometheus监控**页面的顶部菜单栏，选择地域，然后单击**新建Prometheus实例**。

4.  在**新建Prometheus实例**页面，单击**ECS集群（VPC）**区域。

5.  在接入 ECS集群\(VPC\)面板的目标VPC右侧操作列，单击**卸载**。

6.  在弹出的**提示**对话框中，单击**确认**。

    卸载成功后，对应VPC右侧状态列显示未安装。

    ![vpc安装成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6532475261/p292834.png)


