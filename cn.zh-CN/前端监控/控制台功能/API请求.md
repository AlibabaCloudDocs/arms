# API请求

API请求提供应用中每个API的调用情况，包括调用成功率、返回信息、调用成功或失败的平均耗时等。

## 功能介绍

阿里云ARMS前端监控的API请求模块，可清晰展示以下信息：

-   每个API的成功率
-   API返回信息
-   API接口的调用成功平均耗时
-   API接口的调用失败平均耗时

此外，该模块还会展示上述统计数据在以下维度上的分布情况：

-   地理
-   浏览器
-   操作系统
-   设备
-   分辨率
-   版本

## API成功率

左侧的成功率页签展示的是API调用成功率排行。右侧API成功率区域展示的是左侧列表选中的API在指定时间范围内的调用量和调用成功率曲线，API链路追踪（TOP 20）区域展示的是该API调用成功或失败的链路TOP 20，单击**操作**列的**链路追踪**和**访问明细**，可以查看对应链路的调用链路详情和访问明细。

![API成功率](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43657.png)

## API返回信息

左侧的Msg聚类页签展示的是API返回信息排行。右侧的Msg调用详情区域展示的是左侧列表选中的返回信息的API调用列表，按调用量降序排列。

![Msg调用详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43661.png)

## API成功耗时

左侧的成功耗时页签展示的是API调用成功时的平均耗时。右侧的API成功耗时区域展示的是左侧列表选中的API的调用成功平均耗时曲线和调用成功次数柱形图。

![API成功耗时](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43666.png)

## API失败耗时

左侧的失败耗时页签展示的是API调用失败时的平均耗时。右侧的API失败耗时区域展示的是左侧列表选中的API的调用失败平均耗时曲线和调用失败次数柱形图。

![API失败耗时](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p187055.png)

## 地理分布

在**地理分布**模块，您可以查看上述统计信息的地理分布情况。地理分布又分为中国和世界两个维度，中国维度的单位为省，世界维度的单位为国家/地区。

![API地理分布](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43635.png)

## 终端分布

在**终端分布**模块中，您可以查看上述统计信息的终端分布情况。终端分布又细分为浏览器、操作系统、设备、分辨率等维度。

![API终端分布](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43638.png)

## 版本分布

在**版本分布**模块中，您可以查看上述统计信息的宿主版本号和应用版本号。

![API版本分布](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p187056.png)

## 通用操作

在API请求模块中，您可以执行以下通用操作。

-   在左侧页签上，单击页签上的上箭头或下箭头来改变列表的排列顺序。上箭头表示升序，下箭头表示降序。
-   在右侧的详情显示区域中，单击右上角的列表图标，可在图表和表格视图间切换。

    ![API成功率-列表模式](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43639.png)

-   在右侧的详情显示区域中，单击右上角的时钟图标，可指定时间范围。

    ![API时间指定范围](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1629786061/p43644.png)


