# Deployment详情

本文介绍了Deployment资源的详细信息。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**容器监控**。

3.  在顶部菜单栏，选择地域。

4.  在**容器监控**页面，单击Kubernetes集群名称。

5.  在总览页面的命名空间区域单击目标命名空间和资源的交点。

    **说明：**

    -   单击蓝色区域，进入所有资源列表。
    -   单击红色区域，进入异常资源列表。
6.  在资源列表页面，单击Deployment页签。

7.  在Deployment页签，单击目标Deployment名称。

8.  在Deployment详情页面右上角的时间选择框内设置需要查看的时间段。


## 基本信息

在Deployment基本信息区域显示Deployment的请求数、错误数、平均响应时间、慢调用次数、当前Pod数和运行时长。

![容器监控Deployment详情基本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9230193261/p280239.png)

在基本信息区域，您可以执行以下操作：

-   单击**开启应用监控**，在弹出的对话框中单击**确认**，可以开启应用监控。开启应用监控后，单击**查看应用性能**，可以查看Deployment的应用性能情况。更多信息，请参见[应用总览](/cn.zh-CN/应用监控/控制台功能/应用总览.md)。

    **说明：**

    -   仅Java和PHP语言的应用支持开启应用监控，即Deployment的Pod中至少有一个Container是Java语言或者PHP语言。
    -   开启应用监控前，请先安装应用监控的ack-arms-pilot组件。具体操作，请参见[接入容器监控](/cn.zh-CN/容器监控/容器监控接入/接入容器监控.md)。
-   单击**查看YAML**，查看Deployment的YAML文件内容。

## 请求数、响应时间、错误数和慢调用数

容器监控支持对多个协议的请求数、响应时间、错误数和慢调用数进行监控。

单击协议的名称，可以查看不同协议对应的请求数、响应时间、错误数和慢调用数。各协议可查看指标的详细信息，请参见[多协议指标详情]()。

![容器监控HTTP协议指标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6200375261/p292619.png)

## Pod列表

在Pod列表区域显示当前Deployment下的所有Pod，以及Pod的请求数、错误数、平均响应时间、CPU使用率、内存使用率、所属Node、运行时长和状态，并显示了请求数、错误数和平均响应时间的时序曲线。

![容器监控-Service关联Pod列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p275739.png)

在Pod列表区域，您可以执行以下操作：

-   单击请求数、错误数、平均响应时间、CPU使用率和内存使用率右侧的![排序](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8987912261/p278362.png)图标，可以分别按请求数、错误数和平均响应时间排序。
-   将鼠标悬浮于请求数、错误数和平均响应时间的时序曲线上，可以查看对应时间点具体的数值。
-   单击Pod名称，可以查看目标Pod详情。更多信息，请参见[Pod详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Pod详情.md)。
-   单击Node名称，可以查看目标Node详情。更多信息，请参见[Node详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Node详情.md)。

## 拓扑

在拓扑区域显示了Deployment上下游的拓扑关系。更多信息，请参见[查看集群网络拓扑](/cn.zh-CN/容器监控/使用教程/探索/查看集群网络拓扑.md)。

![容器监控-service详情拓扑](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5067093261/p278369.png)

## Conditions

在Deployment的Conditions区域显示了Deployment的下所有Conditions的名称、运行状态、上次转换事件、原因和信息。

![容器监控Deployment详情conditions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0048093261/p280271.png)

## 联系我们

如果您在使用容器监控中有任何问题，请联系容器服务答疑钉钉群（群号：`31588365`）获取帮助。

