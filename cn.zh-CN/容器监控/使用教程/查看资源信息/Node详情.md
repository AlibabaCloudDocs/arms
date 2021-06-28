# Node详情

本文介绍了Node资源的详细信息。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**容器监控**。

3.  在顶部菜单栏，选择地域。

4.  在**容器监控**页面，单击Kubernetes集群名称。

5.  在总览页面的Node资源概览区域单击**查看全部Node**。

6.  在Node列表页面，单击目标Node名称。

7.  在Node详情页面右上角的时间选择框内设置需要查看的时间段。


## 基本信息

在Node基本信息区域显示Node的CPU使用率、CPU请求率、内存使用率、内存请求率、内存限制率、磁盘使用率和网络流量。

![容器监控Node详情基本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280302.png)

在基本信息区域，您可以执行以下操作：

单击**查看YAML**，查看Node的YAML文件内容。

## CPU

CPU区域显示了Node CPU容量，以及CPU使用率、CPU请求率和CPU限制率的时序曲线。

![容器监控Node详情CPU](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280316.png)

在CPU区域，您可以执行以下操作：

-   将鼠标悬浮于CPU的时序曲线上，可以查看对应时间点具体的数值。
-   单击指标名称，可以隐藏对应的时序曲线。

## 内存

内存区域显示了Node内存容量，以及内存使用率、请求率和限制率的时序曲线。

![容器监控Node详情内存](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280317.png)

在内存区域，您可以执行以下操作：

-   将鼠标悬浮于内存的时序曲线上，可以查看对应时间点具体的数值。
-   单击指标名称，可以隐藏对应的时序曲线。

## 磁盘

磁盘区域显示了Node磁盘使用率的时序曲线。

![容器监控Node详情磁盘](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280318.png)

在磁盘区域，您可以执行以下操作：

将鼠标悬浮于内存的时序曲线上，可以查看对应时间点具体的数值。

## 网络

网络区域显示了Node网络流入流量和流出流量的时序曲线。

![容器监控Node详情流量](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280319.png)

在网络区域，您可以执行以下操作：

-   将鼠标悬浮于内存的时序曲线上，可以查看对应时间点具体的数值。
-   单击指标名称，可以隐藏对应的时序曲线。

## Pod列表

在Pod列表区域显示当前Node下的所有Pod，以及Pod的CPU使用情况、CPU请求率、CPU限制率、内存使用情况、内存请求率、内存限制率、运行时长和状态。

![容器监控Node详情当前Pod详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280412.png)

在Pod列表区域，您可以执行以下操作：

-   单击CPU使用、CPU请求率、CPU限制率、内存使用、内存请求率、内存限制率右侧的![排序](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8987912261/p278362.png)图标，可以分别按对应指标排序。
-   单击Pod名称，可以查看目标Pod详情。更多信息，请参见[Pod详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Pod详情.md)。

## Conditions

Conditions区域显示了Node的下所有Conditions的名称、运行状态、上次转换事件、原因和信息。

![容器监控Deployment详情conditions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280271.png)

## 联系我们

如果您在使用容器监控中有任何问题，请联系容器服务答疑群（群号：`31588365`）获取帮助。

