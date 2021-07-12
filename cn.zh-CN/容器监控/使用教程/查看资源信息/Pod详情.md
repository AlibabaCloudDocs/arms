# Pod详情

本文介绍了Pod资源的详细信息。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**容器监控**。

3.  在顶部菜单栏，选择地域。

4.  在**容器监控**页面，单击Kubernetes集群名称。

5.  在总览页面的命名空间区域单击目标命名空间和资源的交点。

    **说明：**

    -   单击蓝色区域，进入所有资源列表。
    -   单击红色区域，进入异常资源列表。
6.  在资源列表页面，单击Pod页签。

7.  在Pod页签，单击目标Pod名称。

8.  在Pod详情页面右上角的时间选择框内设置需要查看的时间段。


## 基本信息

在Pod基本信息区域显示Pod的请求数、错误数、平均响应时间、慢调用次数、当前容器数、重启次数和运行时长。

![容器监控Pod详情基本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3319093261/p280209.png)

在基本信息区域，您可以执行以下操作：

-   单击**日志**，可以查看当前Pod的日志信息。
-   将鼠标悬浮于**终端**上，可以查看Pod的Container列表。单击Container名称，可以登录对应Container的终端。

## 请求数、响应时间、错误数和慢调用数

容器监控支持对多个协议的请求数、响应时间、错误数和慢调用数进行监控。

单击协议的名称，可以查看不同协议对应的请求数、响应时间、错误数和慢调用数。各协议可查看指标的详细信息，请参见[多协议指标详情](/cn.zh-CN/容器监控/参考信息/多协议指标详情.md)。

![容器监控HTTP协议指标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6200375261/p292619.png)

## CPU和Memory

在Pod的CPU和Memory区域显示了Pod的CPU和内存的使用量、请求量、限制量以及对应的时序曲线。

![容器监控Pod详情CPU和Memory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3319093261/p280213.png)

在CPU和Memory区域，您可以执行以下操作：

-   将鼠标悬浮于CPU和Memory使用量的时序曲线上，可以查看对应时间点具体的数值。

-   单击曲线右上角的使用量、请求量、限制量指标，可以显示或隐藏对应曲线。

## Container列表

在Pod的Container列表区域显示了Pod的下所有Container的名称、运行状态、信息、CPU使用量和Memory使用量。

![容器监控Pod详情container](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3319093261/p280217.png)

在Container列表区域，您可以执行以下操作：

单击Container名称，可以查看Container的详细信息，更多信息，请参见[Container详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Container详情.md)。

## Conditions

在Pod的Conditions区域显示了Pod下所有Conditions的名称、运行状态、上次转换事件、原因和信息。

![容器监控Pod详情Conditions ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4319093261/p280233.png)

## Node

在Pod的Node区域显示了Pod关联的Node的CPU使用率、内存使用率、磁盘使用率和网络流量的时序曲线。

![容器监控-Pod-Node列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4319093261/p284129.png)

在Node区域，您可以执行以下操作：

-   单击Node名称，可以查看Node的详细信息。更多信息，请参见[Node详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Node详情.md)。
-   将鼠标悬浮于CPU使用率、内存使用率、磁盘使用率和网络流量的时序曲线上，可以查看对应时间点具体的数值。

## 联系我们

如果您在使用容器监控中有任何问题，请联系容器服务答疑钉钉群（群号：`31588365`）获取帮助。

