# 查看Insights巡检结果

Insights支持对不同地域的不同应用进行定时巡检，并且可以针对巡检到的问题给出具体的根因分析和建议。本文介绍如何查看Insights巡检结果。

已创建应用监控，具体操作，请参见[应用监控接入概述](/cn.zh-CN/应用监控/接入应用监控/应用监控接入概述.md)。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Insights**。

3.  在顶部菜单栏，选择地域。

4.  在Insights页面右上角的时间选择框，选择需要查看的时间段。

5.  在Insights页面顶部的下拉框选择需要查看的应用。

    **说明：** 默认查看全部应用。


## 问题分类和问题类型

问题分类和问题类型区域显示了当前巡检到的问题对应的问题分类和问题类型的数量。

![Insights-问题类型](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7355352261/p274864.png)

在问题分类和问题类型区域，您可以执行以下操作：

选中或取消选中不同分类或类型的问题，在问题数和问题列表区域显示或隐藏对应的问题。问题的详细说明，请参见[t2084874.md\#]()。

## 问题数

问题数区域显示了所有问题类型在各时间点的分布情况。

![Insights-问题数](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7355352261/p274834.png)

在问题数区域，您可以执行以下操作：

-   将鼠标悬浮于柱状图上，显示对应时间点上各问题类型的具体问题数。
-   单击图例，隐藏或显示数据。

## 问题列表

问题列表区域显示了所有问题名称、发生次数、开始时间和结束时间。

![Insights问题列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7355352261/p274871.png)

在问题列表区域，您可以执行以下操作：

单击问题所在行，可以展开目标问题的发生记录。单击详情列的链接，查看单次问题发生时的详细信息。更多信息，请参见[Insights详情](#section_zje_qh2_ysx)。

## Insights详情

Insights详情页面显示了单次问题发生时的发现依据、问题定界和问题根因分析。

![Insights详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4492172261/p279192.png)

在Insights详情页面，您可以执行以下操作：

-   单击异常服务名称，可以查看服务的详细信息。
-   单击根因分析区域的链接，在根因分析面板可以查看问题总结和建议，以及产生问题的具体原因。

    ![Insights根因分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5492172261/p280121.png)


