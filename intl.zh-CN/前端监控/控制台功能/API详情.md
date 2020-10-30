# API详情

API详情页提供指定时间段内应用中所有API请求的成功率、平均成功耗时、平均失败耗时、缓慢次数、错误次数，并以API请求发起端的地域、域名、网络制式等维度展示统计数据。

## 功能入口



1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。
2.  在左侧导航栏单击**前端监控**。
3.  在**前端监控**页面的应用列表中单击目标应用。
4.  在左侧导航栏中单击**API详情**，跳转至API详情页面。

    本文将页面划分为3个区域进行说明。

    ![API details](../images/p111559.png "API详情")


## 筛选条件

通过设置不同维度的筛选条件，查看相应的API信息。可筛选的维度包括**API**、**返回信息**、**HTTP状态码**、**页面**、**地域**、**操作系统**、**域名**、**网络制式**、**设备**、**浏览器**。

将鼠标悬浮于一个筛选框中，单击右侧的![delete](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3267633061/p175853.png)，可删除该条件的选择。单击最右侧的重置，可清除所有筛选条件。

![API details filter](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2228683061/p111568.png)

## 成功率

在API请求信息页签选择**成功率**，可以查看成功率、调用成功次数、错误次数和错误用户数。

![success](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177857.png)

-   成功率：以折线图显示指定时间段内应用中所有API请求的成功率，对应右侧纵坐标。
-   调用成功次数：以蓝色柱状图显示指定时间段内每小时的调用次数，对应左侧纵坐标。
-   错误次数：以黄色柱状图显示指定时间段内每小时的调用错误次数，对应左侧纵坐标。

将鼠标悬浮于柱状图上，可查看指定时间段内的具体的成功率、调用成功次数、错误次数和错误用户数。

## 成功耗时或失败耗时

在API请求信息页签选择**成功耗时**或**失败耗时**，可以查看平均成功耗时或平均失败耗时、≤1000ms的调用次数和≥1000ms的调用次数。

![time](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177858.png)

-   平均成功耗时或平均失败耗时：以折线图显示指定时间段内应用中所有API的平均成功耗时或平均失败耗时，对应右侧纵坐标。
-   ≤1000ms的调用次数：以蓝色柱状图显示每小时≤1000ms的成功调用总次数或失败调用总次数，对应左侧纵坐标。
-   ≥1000ms的调用次数：以黄色柱状图显示每小时≥1000ms的成功调用总次数或失败调用总次数，对应左侧纵坐标。

## 缓慢次数

**说明：** 缓慢次数是指耗时\>1000ms的调用次数。

在API请求信息页签选择**缓慢次数**，可以查看缓慢次数。

![slow](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177859.png)

缓慢次数以柱状图显示指定时间段内应用中所有API的缓慢请求次数，对应左侧纵坐标。

## 错误次数

在API请求信息页签选择**错误次数**，可以查看错误次数。

![error](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177880.png)

错误次数以柱状图显示指定时间段内应用中所有API的错误请求次数，对应左侧纵坐标。

## API请求列表

在区域③中选择**API请求列表**，可以查看各API在指定时间段内的请求情况。

![API ask](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177860.png)

-   单击列表首行中的属性右侧的图标，可对列表进行排序。
-   将鼠标悬浮于**API**列的API别名上，单击![edit](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1397593061/p177320.png)，可以修改API别名，修改后，所有API将会以别名展示。单击**设置为搜索值**，可以将该API设置为筛选项。
-   单击**错误次数**列的数字，可以查看指定时间段内错误请求详情和错误分布情况。 单击请求详情区域的**查看会话**，可以查看错误请求的会话追踪详情。

    ![error details](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6039683061/p111587.png)

-   单击**缓慢次数**列的数字，显示指定时间段内缓慢请求详情和缓慢请求分布情况。 在请求详情区域，单击**查看调用链**。可以查看缓慢请求的调用链路和业务轨迹。单击**查看会话**，可以查看缓慢请求的会话追踪详情。

    ![error details](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6039683061/p111588.png)

-   单击右侧**操作**列的**分析**，可以查看API详情、API错误详情、API缓慢详情和分布情况。

    ![analysis](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177862.png)

    -   在API详情页面，可以查看API请求成功率和请求详情。在请求详情区域，单击**查看调用链**。可以查看该API的调用链路和业务轨迹。单击**查看会话**，可以查看该API的会话追踪详情。
    -   在API错误详情页面，可以查看错误次数分布和请求详情。
    -   在API缓慢详情页面，可以查看响应时间分布和网络请求信息。
    -   在分布页面，可以查看返回信息、HTTP状态码、页面、域名和地理分布信息，并可以查看操作系统、浏览器、设备和网络制式各维度的占比。

## 返回信息列表

在区域③中选择**返回信息列表**，可以查看各API的所有返回信息。

![reback](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1397593061/p177186.png)

-   单击列表首行中的属性右侧的图标，可对列表进行排序。
-   将鼠标悬浮于**返回信息**列的返回信息上，单击**设置为搜索值**，可以将该返回信息设置为筛选项。
-   单击**缓慢次数**列的数字，显示指定时间段内缓慢请求详情和缓慢请求分布情况。 在请求详情区域，单击**查看调用链**。可以查看缓慢请求的调用链路和业务轨迹。单击**查看会话**，可以查看缓慢请求的会话追踪详情。

    ![Slow times](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1397593061/p177282.png)

-   单击右侧**操作**列的**分析**，可以查看API详情、API错误详情、API缓慢详情和分布情况。
    -   在API详情页面，可以查看API请求成功率和请求详情。在请求详情区域，单击**查看调用链**。可以查看该API的调用链路和业务轨迹。单击**查看会话**，可以查看该API的会话追踪详情。
    -   在API错误详情页面，可以查看错误次数分布和请求详情。
    -   在API缓慢详情页面，可以查看响应时间分布和网络请求信息。
    -   在分布页面，可以查看返回信息、HTTP状态码、页面、域名和地理分布信息，并可以查看操作系统、浏览器、设备和网络制式各维度的占比。

        ![distributed](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1620404061/p177958.png)


## HTTP状态码

在区域③中选择**HTTP状态码**，可以查看所有的HTTP状态码。

![HTTP](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1397593061/p177332.png)

-   单击列表首行中的属性右侧的图标，可对列表进行排序。
-   将鼠标悬浮于**HTTP状态码**列的HTTP状态码上，单击**设置为搜索值**，可以将该HTTP状态码设置为筛选项。
-   单击**缓慢次数**列的数字，显示指定时间段内缓慢请求详情和缓慢请求分布情况。 在请求详情区域，单击**查看调用链**。可以查看缓慢请求的调用链路和业务轨迹。单击**查看会话**，可以查看缓慢请求的会话追踪详情。

    ![Slow times](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1397593061/p177282.png)

-   单击右侧**操作**列的**分析**，可以查看API详情、API错误详情、API缓慢详情和分布情况。
    -   在API详情页面，可以查看API请求成功率和请求详情。在请求详情区域，单击**查看调用链**。可以查看该API的调用链路和业务轨迹。单击**查看会话**，可以查看该API的会话追踪详情。
    -   在API错误详情页面，可以查看错误次数分布和请求详情。
    -   在API缓慢详情页面，可以查看响应时间分布和网络请求信息。
    -   在分布页面，可以查看返回信息、HTTP状态码、页面、域名和地理分布信息，并可以 查看操作系统、浏览器、设备和网络制式各维度的占比。

## 分布情况

在区域③中选择**分布情况**，可以查看域名、页面和地理分布信息，并可以查看操作系统、浏览器、设备和网络制式各维度的占比。将鼠标悬浮于**域名**或**页面**列上，单击**设置为搜索值**，可以将该域名或页面设置为筛选项。

**说明：**

-   只有操作系统和浏览器支持版本号分布。
-   操作系统、浏览器、设备和网络制式饼图只展示Top5的维度分布，单击各区域右上角的切换视图，可查看该维度所有类别占比情况。

![distributed](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2620404061/p177360.png)

