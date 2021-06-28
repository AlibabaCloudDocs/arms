# DaemonSet详情

本文介绍了DaemonSet资源的详细信息。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**容器监控**。

3.  在顶部菜单栏，选择地域。

4.  在**容器监控**页面，单击Kubernetes集群名称。

5.  在总览页面的命名空间区域单击目标命名空间和资源的交点。

    **说明：**

    -   单击蓝色区域，进入所有资源列表。
    -   单击红色区域，进入异常资源列表。
6.  在资源列表页面，单击DaemonSet页签。

7.  在DaemonSet页签，单击目标DaemonSet名称。

8.  在DaemonSet详情页面右上角的时间选择框内设置需要查看的时间段。


## 基本信息

在DaemonSet基本信息区域显示DaemonSet的请求数、错误数、平均响应时间、慢调用次数、当前Pod数和运行时长。

![容器监控DaemonSet](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7910193261/p280274.png)

在基本信息区域，您可以执行以下操作：

单击**查看YAML**，查看DaemonSet的YAML文件内容。

## 请求数

在DaemonSet的请求数区域显示了DaemonSet请求数的时序曲线和Top接口列表。

![容器监控-Service详情的请求数和响应时间](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p275743.png)

在请求数区域，您可以执行以下操作：

-   将鼠标悬浮于请求数的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看DaemonSet请求数的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## 响应时间

在DaemonSet的响应时间区域显示了DaemonSet平均响应时间和P95响应时间的时序曲线，以及Top接口列表。

![容器监控Service详情平均响应时间](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p284103.png)

在响应时间区域，您可以执行以下操作：

-   将鼠标悬浮于响应时间的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看DaemonSet响应时间的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## 错误数和慢调用

在DaemonSet的错误数和慢调用区域显示了DaemonSet错误数和慢调用的时序曲线，以及Top接口列表。

![容器监控-Service详情的错误数和慢调用](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7397912261/p275751.png)

在错误数和慢调用区域，您可以执行以下操作：

-   将鼠标悬浮于错误数和慢调用的时序曲线上，可以查看对应时间点具体的数值。
-   使用光标选中一段时间，可以查看指定时间段的统计情况。
-   在Top列表区域可以选择查看DaemonSet错误数和慢调用的Top 5、Top 10或Top 15接口，单击目标接口右侧的**查看列表**，可以查看目标接口关联的接口信息。更多信息，请参见[接口详情](#section_nr2_tn5_qr4)。

## Pod列表

在Pod列表区域显示当前DaemonSet下的所有Pod，以及Pod的请求数、错误数、平均响应时间、CPU使用率、内存使用率、所属Node、运行时长和状态，并显示了请求数、错误数和响应时间的时序曲线。

![容器监控-Service关联Pod列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p275739.png)

在Pod列表区域，您可以执行以下操作：

-   单击请求数、错误数、平均响应时间、CPU使用率和内存使用率右侧的![排序](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8987912261/p278362.png)图标，可以分别按请求数、错误数和响应时间排序。
-   将鼠标悬浮于请求数、错误数和响应时间的时序曲线上，可以查看对应时间点具体的数值。
-   单击Pod名称，可以查看目标Pod详情。更多信息，请参见[Pod详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Pod详情.md)。
-   单击Node名称，可以查看目标Node详情。更多信息，请参见[Node详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Node详情.md)。

## 拓扑

在拓扑区域显示了DaemonSet上下游的拓扑关系。更多信息，请参见[查看集群网络拓扑](/cn.zh-CN/容器监控/使用教程/探索/查看集群网络拓扑.md)。

![容器监控-service详情拓扑](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p278369.png)

## 接口详情

在接口详情面板显示了接口被调用的记录，并显示调用的产生时间、耗时、状态码和Trace ID。

![容器监控-service详情-接口详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7397912261/p278370.png)

在接口详情区域，您可以执行以下操作：

单击调用记录右侧的**查看详情**，可以查看目标调用记录的请求URL、Hearders、Body，响应Headers、Body、StatusCode，调用拓扑，调用各阶段的执行结果、耗时和速度。

## 联系我们

如果您在使用容器监控中有任何问题，请联系容器服务答疑群（群号：`31588365`）获取帮助。

