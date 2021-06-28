# Node列表

本文展示了目标集群下的Node列表。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**容器监控**。

3.  在顶部菜单栏，选择地域。

4.  在**容器监控**页面，单击目标Kubernetes集群名称。

5.  在总览页面的Node资源概览区域单击**查看全部Node**。

6.  在Node列表页面右上角的时间选择框内设置需要查看的时间段。

    在Node列表页面可以查看Node的名称、标签、当前Pod数、CPU使用率、CPU请求率、内存使用率、内存请求率、磁盘使用率、状态。

    Node列表默认按状态排序，状态栏显示的是Node的异常程度，颜色对应如下：

    -   红色：严重（Fatal）。
    -   蓝色：正常（Normal）。

## Node

**Node**列表显示了所有Node的名称、标签、当前Pod数、CPU使用率、CPU请求率、内存使用率、内存请求率、磁盘使用率、状态。

![容器监控-Node列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1138093261/p275712.png)

在Node列表，您可以执行以下操作：

-   通过设置Node名称、状态和标签值，可以对Node进行筛选。
-   单击Node名称，查看目标Node详情。更多信息，请参见[Node详情](/cn.zh-CN/容器监控/使用教程/查看资源信息/Node详情.md)。
-   单击当前Pod数的数值，查看目标Node关联的Pod列表。更多信息，请参见[Pod列表](/cn.zh-CN/容器监控/使用教程/查看资源信息/资源列表.md)。

## 联系我们

如果您在使用容器监控中有任何问题，请联系容器服务答疑群（群号：`31588365`）获取帮助。

