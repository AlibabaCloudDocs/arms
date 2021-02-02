# 使用SkyWalking和链路追踪进行代码级慢请求分析

借助Java字节码注入技术，许多基于Java的框架可以实现自动埋点，从而帮助您了解慢请求具体发生在哪两个埋点之间，但这不足以定位代码层的问题。如需精确定位导致慢请求出现的代码方法，您可以搭配使用SkyWalking的慢请求分析功能和链路追踪。

您已通过SkyWalking接入链路追踪，详情请参见[通过SkyWalking上报Java应用数据](/cn.zh-CN/准备工作/开始监控Java应用/通过SkyWalking上报Java应用数据.md)。

SkyWalking采集慢请求数据的工作流程如图所示。

![dg_skywalking_slow_request_analysis_how_it_works](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192607951/p139682.png)

**说明：** 仅SkyWalking 7.0及更高版本具备慢请求分析功能。

## 创建慢请求采集任务

1.  登录[链路追踪Tracing Analysis控制台](https://tracing.console.aliyun.com/)[链路追踪Tracing Analysis控制台](https://tracing-sg.console.aliyun.com/)。

2.  在左侧导航栏单击**应用列表**，在页面左上角选择目标地域，并在**应用列表**页面单击目标应用的名称。

3.  在左侧导航栏单击**慢请求分析**，并单击**新建任务**。

4.  在**新建任务**对话框中输入以下信息，并单击**确认**。

    ![新建慢请求分析任务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192607951/p139671.png)

    |参数|描述|是否必填|示例值|
    |--|--|----|---|
    |Span名称|需监控的Span。|是|/api|
    |监控时间|开始监控的时间。可选择**此刻**，或选择**设置时间**并设置一个自定义时间。|否|此刻|
    |监控持续时间|监控持续的时间。|否|5 min|
    |Span耗时阈值|仅分析耗时超过该阈值的Span。单位为ms。|否|30 ms|
    |监控间隔|采集监控数据的时间间隔。|否|20 ms|
    |最大采样数|被采集数据的Span最大数量。取值范围为1~9。|否|5|

    创建好的任务将显示在**任务列表**中。


## 定位导致慢请求出现的方法

以您设置的监控时间为起点，经过指定的监控持续时间后，耗时超过阈值的Span将显示在**Sampled Traces**区域。请按照以下步骤在页面右侧的线程栈详细信息定位导致慢请求出现的方法。

1.  在**慢请求分析**页面的**任务列表**区域单击目标任务。

    ![慢请求分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192607951/p139677.png)

    耗时超过阈值的Span将显示在**Sampled Traces**区域。

2.  在**Sampled Traces**区域单击目标Span，并观察页面右侧的**线程栈**区域。

    以红色字体显示的方法名即为耗时超过所设置阈值的方法。您可以针对性地优化这些方法。


## 为什么监控持续时间结束后未采样到任何线程栈？

如果监控持续时间结束后未采样到任何线程栈，请按照以下步骤排查。

1.  在**慢请求分析**页面的**任务列表**区域单击目标任务右侧的**查看任务详情**。

2.  在**任务详情**对话框的**日志**区域查看详细信息。

    ![db_slow_request_analysis_job_details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4192607951/p139680.png)

    -   如果**实例**字段末尾含有监控的Agent IP地址，且**操作类型**为`EXECUTION_FINISHED`或`EXECUTION_NOTIFY`，则说明网络连接正常，只是因为没有耗时超过阈值的Span。
    -   如果不符合上述描述，则说明网络连接有问题，请稍后重试。

**相关文档**  


[博客：在线代码级性能剖析方面补全分布式追踪的最后一块短板](http://skywalking.apache.org/zh/blog/2020-03-23-using-profiling-to-fix-the-blind-spot-of-distributed-tracing.html)

