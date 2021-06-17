# Container详情

本文介绍了Container资源的详细信息。

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

8.  在Pod详情页面的Container区域单击目标Container名称。


## 基本信息

在Container基本信息区域显示Container的请求数、错误数、平均响应时间、慢调用次数、当前容器数、重启次数和运行时长。

![容器监控Container详情基本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2432193261/p280276.png)

在基本信息区域，您可以执行以下操作：

-   单击**日志**，可以查看Container的日志信息。
-   单击**终端**，可以登录Container的终端。

## 请求数

在Container的请求数区域显示了Container请求数的时序曲线和Top接口列表。

![容器监控-Service详情的请求数和响应时间](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p275743.png)

在请求数区域，您可以执行以下操作：

-   将鼠标悬浮于请求数的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看Container请求数的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## 响应时间

在Container的响应时间区域显示了Container平均响应时间和P95响应时间的时序曲线，以及Top接口列表。

![容器监控Service详情平均响应时间](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p284103.png)

在响应时间区域，您可以执行以下操作：

-   将鼠标悬浮于响应时间的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看Container响应时间的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## 错误数和慢调用

在Container的错误数和慢调用区域显示了Container错误数和慢调用的时序曲线，以及Top接口列表。

![容器监控-Service详情的错误数和慢调用](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7397912261/p275751.png)

在错误数和慢调用区域，您可以执行以下操作：

-   将鼠标悬浮于错误数和慢调用的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看Container错误数和慢调用的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## CPU和Memory

在Container的CPU和Memory区域显示了Container的CPU和内存的使用量、请求量、限制量以及使用量的时序曲线。

![容器监控Pod详情CPU和Memory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3319093261/p280213.png)

在CPU和Memory区域，您可以执行以下操作：

-   将鼠标悬浮于CPU和Memory使用量的时序曲线上，可以查看对应时间点具体的数值。

-   单击曲线右上角的使用量、请求量、限制量指标，可以显示或隐藏对应曲线。

## CPU Throttled和内存FailCnt

CPU Throttled区域显示了CPU使用量超过Limit从而被限制的CPU数量。

内存FailCnt区域显示了内存使用量超过Limit从而申请内存失败的次数。

![容器监控Container详情 CPU Throttled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2432193261/p280291.png)

在CPU Throttled和内存FailCnt区域，您可以执行以下操作：

将鼠标悬浮于CPU Throttled和内存FailCnt的时序曲线上，可以查看对应时间点具体的数值。

## Node

Node区域显示了容器所在的Node信息，包括Node名称，CPU使用率、内存使用率、磁盘使用率和网络流量的时序曲线。

![容器监控Container详情Node](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2432193261/p280297.png)

在Node区域，您可以执行以下操作：

-   单击Node名称，可以查看Node的详细信息。更多信息，请参见[Node详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Node详情.md)。
-   将鼠标悬浮于CPU使用率、内存使用率、磁盘使用率和网络流量的时序曲线上，可以查看对应时间点具体的数值。

## 接口详情

在接口详情面板显示了接口被调用的记录，并显示调用的产生时间、耗时、状态码和Trace ID。

![容器监控-service详情-接口详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7397912261/p278370.png)

在接口详情区域，您可以执行以下操作：

单击调用记录右侧的**查看详情**，可以查看目标调用记录的请求URL、Hearders、Body，响应Headers、Body、StatusCode，调用拓扑，调用各阶段的执行结果、耗时和速度。

