# Agent设置

在Agent设置页签可以查看健康检查结果、设置Agent副本数和升级Agent。

您的服务已接入Prometheus监控。具体操作，请参见[开始使用Prometheus监控]()。

## 查看健康检查结果

健康检查功能可以检查阿里云Prometheus监控是否安装成功。如果您发现Prometheus监控无法监控到数据，那么可以根据健康检查结果排查原因。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在顶部菜单栏，选择地域。

4.  在**Prometheus监控**页面，单击K8s集群名称。

5.  在左侧导航栏单击**设置**，在右侧页面单击**Agent设置**页签。


在Agent设置页签，您可以查看健康检查结果。

![健康检查](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3161674161/p245298.png)

健康检查结果主要是Prometheus监控各个阶段的运行数据，包括：

-   Grafana创建情况。
-   API请求情况。

    **说明：** 自定义创建的Grafana大盘和除K8s集群外的自建集群通过API URL获取数据源。

-   Kubernetes集群运行时状态采集情况。
-   Prometheus Agent采集个数及详情。
-   采集指标对应的采集任务（Job）个数及详情。此项内容可以查看哪些采集任务（Job）是免费或者收费。
-   Promethues Metric的使用情况。

## 设置Agent副本数

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在顶部菜单栏，选择地域。

4.  在**Prometheus监控**页面，单击K8s集群名称。

5.  在左侧导航栏单击**设置**，在右侧页面单击**Agent设置**页签。

6.  在Agent设置页签，单击右上角的**设置Agent副本数**。

7.  在弹出的设置Agent副本数对话框中设置副本数，然后单击**确认**。

    一个Agent的采集能力约为20万条数据/分钟，所需资源为200 MB~900 MB内存和1核CPU。一般情况下副本数为1即可满足需求。假设一个集群每分钟产生160万条数据，则需要将副本数设为8。


## 升级Agent

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在顶部菜单栏，选择地域。

4.  在**Prometheus监控**页面，单击K8s集群名称。

5.  在左侧导航栏单击**设置**，在右侧页面单击**Agent设置**页签。

6.  在Agent设置页签，单击右上角的**升级Agent**。

    运行结束弹出执行结果对话框。

    ![Agent设置-升级Agent](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4161674161/p245297.png)


