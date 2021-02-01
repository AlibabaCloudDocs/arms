# SQL调用分析

本文说明如何查看SQL调用分析，从而了解应用的SQL调用情况。

[接入应用监控](/intl.zh-CN/应用监控/接入应用监控/应用监控接入概述.md)

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**应用监控** \> **应用列表**。

3.  在顶部菜单栏，选择地域。

4.  在**应用列表**页面，单击应用名称。

5.  在**左侧导航栏**，单击**应用详情**。

6.  在**应用详情**页面，选择应用实例，设置时间段，单击**SQL调用分析**页签。

    ![查看sql调用分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0443191161/p230688.png)


## SQL调用统计

**SQL调用统计**区域显示该应用在指定时间段的SQL调用时序曲线。

![SQL调用统计](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0443191161/p232883.png)

1.  在**SQL调用统计**页签下，您可以执行以下操作：

    -   将光标移到统计图上，查看统计情况。
    -   单击![chart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9617031161/p230753.png)图标，查看该指标在某个时间段的统计情况或对比不同日期同一时间段的统计情况。
    -   单击![code](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7567031161/p230759.png)图标，查看该指标的API详情。

## SQL语句列表

SQL语句列表显示该应用在指定时间段的所有SQL语句的列表。

![SQL语句列表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0443191161/p235824.png)

1.  在SQL语句列表，您可以执行以下操作：

    -   在SQL语句的**操作**列，单击**调用统计**，查看该SQL语句的SQL调用时序曲线。
    -   在SQL语句的**操作**列，单击**接口快照**，查看该SQL语句调用的接口的快照。

        接口快照说明，请参见[接口快照]()。


