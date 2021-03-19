# Arthas诊断

Arthas是诊断Java领域线上问题的利器，利用字节码增强技术，可以在不重启JVM进程的情况下，查看程序的运行情况。ARMS白屏化支持Arthas的常用功能，包括JVM概览、线程耗时分析、方法执行分析和性能分析。

要使用Arthas诊断的应用必须满足以下条件：

-   已接入应用监控。如何接入，请参见[应用监控接入概述](/cn.zh-CN/应用监控/接入应用监控/应用监控接入概述.md)。
-   部署环境为Kubernetes。

    **说明：** 本文以容器服务Kubernetes版为例。

-   编程语言为Java。
-   3658端口和8563端口未被占用。

Arthas是一款开源Java诊断工具，深受开发者欢迎。关于Arthas的更多信息，请参见[Arthas官网](https://arthas.aliyun.com/doc/en/)。

## 升级arms-pilot并重启应用

在使用Arthas诊断前，您需要先升级arms-pilot并重启应用。

为容器服务Kubernetes版升级arms-pilot并重启应用的操作步骤如下：

1.  升级arms-pilot。

    1.  登录[容器服务管理控制台](https://cs.console.aliyun.com/)。

    2.  在左侧导航栏，单击**集群**。

    3.  在**集群列表**页面，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。

    4.  在左侧导航栏，选择**工作负载** \> **无状态**。

    5.  在**无状态**页面，从**命名空间**下拉列表，选择arms-pilot-system或arms-pilot，找到探针应用的Deployment，在其右侧**操作**列，选择**更多** \> **重新部署**。

    6.  在**重新部署**对话框，单击**确定**。

2.  如果被监控的应用的PID为1，您需要修改应用的YAML配置文件。

    1.  在**无状态**页面，从**命名空间**下拉列表，选择应用所在命名空间，找到应用的Deployment，在其右侧**操作**列，选择**更多** \> **查看Yaml**。

    2.  在**编辑YAML**对话框，在spec\>template\>metadata\>annotations下添加ArthasEnable: 'on'，然后单击**确定**。

        **说明：** 如果没有metadata下没有annotations，您需要先添加annotations:，然后添加ArthasEnable: 'on'。

        ![编辑YAML](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3966775161/p249474.png)

3.  重启应用。

    1.  在**无状态**页面，从**命名空间**下拉列表，选择应用所在命名空间，找到应用的Deployment，在其右侧**操作**列，选择**更多** \> **重新部署**。

    2.  在**重新部署**对话框，单击**确定**。


## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**应用监控** \> **应用列表**。

3.  在顶部菜单栏，选择地域。

4.  在**应用列表**页面，单击应用名称。

5.  在左侧导航栏，选择**应用诊断** \> **应用诊断-Arthas诊断**。

6.  在Arthas诊断页面，选择应用的Pod。

    ![下载并挂载Arthas](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6617664161/p244901.png)

    -   如果检测未下载Arthas，您需要重新部署探针以下载Arthas。具体操作，请参见[步骤1](#step_yrk_ul5_ywh)。
    -   如果检测未挂载Arthas，ARMS会为您重新部署应用以挂载Arthas。如何手动部署应用，请参见[步骤3](#step_uyy_p4u_17w)。
    -   如果尝试挂载Arthas失败，您需要检查应用的PID：
        -   PID为1：您需要修改应用的YAML配置文件。具体操作，请参见[步骤2](#step_fbo_ip4_7ab)
        -   PID不为1：您可以咨询[技术支持](/cn.zh-CN/.md)。

## JVM概览

JVM概览支持查看应用的JVM相关信息，包括JVM内存、操作系统信息、变量信息等，帮助您了解JVM的总体情况。

1.  Arthas诊断页面默认显示**JVM概览**页签，您可以在**JVM概览**页签下查看以下信息：

    -   **JVM内存**：JVM内存的相关信息，包括堆内存使用情况、非堆内存使用情况、GC情况等。

        ![JVM内存](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8203764161/p244943.png)

    -   **操作系统信息**：操作系统的相关信息，包括平均负载情况，操作系统名称、操作系统版本、Java版本等。

        ![操作系统信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8203764161/p244947.png)

    -   **变量信息**：变量的相关信息，包括系统变量和环境变量。

        ![变量信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8203764161/p244949.png)

    -   **线程Top-10**：CPU使用率排名前10的线程的相关信息，包括名称、ID、CPU使用率、状态。

        ![线程Top-10](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9203764161/p244950.png)

        如需查看某个线程的堆栈信息，您可以在某个线程右侧的**操作**列，单击**查看**。

        ![堆栈详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9203764161/p245000.png)


## 线程耗时分析

线程耗时分析支持显示该应用的所有线程和查看线程的堆栈信息，帮助您快速定位耗时较高的线程。

1.  在Arthas诊断页面，单击**线程耗时分析**页签。

    **线程耗时分析**页签下按照CPU使用率降序显示该应用的所有线程的相关信息，包括线程的名称、ID、CPU使用率、状态。

    ![线程耗时分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9203764161/p245008.png)

2.  如需查看某个线程的堆栈信息，您可以在某个线程右侧的**操作**列，单击**查看**。

    ![堆栈详情](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9203764161/p245000.png)


## 方法执行分析

方法执行分析支持抓取方法的某一次执行的耗时、入参、返回值等信息和钻入，帮助您快速定位导致慢调用的根本原因。方法执行分析适用于调用线下无法复现或日志缺失等场景。

1.  在Arthas诊断页面，单击**方法执行分析**页签。

2.  在**方法执行分析**页签下，选择服务，单击**确定**。

    **说明：** 选择服务后，ARMS将自动推断该服务对应到代码的类和方法，为您自动填写对应的类和方法。如果推断失败，您需要手动填写该服务对应到代码的类和方法。

    方法页签下显示ARMS随机抓取的该方法的某一次执行的信息，包括方法名、执行耗时、入参、返回值、异常以及该方法的内部方法的信息。该方法的内部方法中执行耗时最高的方法的时间轴标红显示。

    ![方法执行分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7471964161/p245017.png)

3.  如需钻入某个内部方法，在其右侧**操作**列，单击**钻入**。

    方法页签下显示该方法的该次执行信息，包括方法名、执行耗时、入参、返回值、异常以及该方法的内部方法的信息。该方法的内部方法中执行耗时最高的方法的时间轴标红显示。

    ![钻入](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8471964161/p245119.png)

4.  如需指定抓取方法的执行的满足条件，执行以下操作：

    1.  在方法页签下，单击**修改诊断参数**。

    2.  在**诊断参数设置**对话框，设置以下参数，然后单击**确认**。

        |参数|描述|示例值|
        |--|--|---|
        |仅当抛出异常|是否仅当方法的执行抛出异常时才抓取。取值：        -   是：仅当方法的执行抛出异常时才抓取。
        -   否：方法的执行不抛出异常时也抓取。
|否|
        |耗时大于|方法的执行耗时大于该耗时才被抓取。单位为ms。|30|
        |对象反序列化层级|方法的执行的参数和返回值为复杂对象时的反序列化深度。取值越大，反序列化深度越深，能看到的复杂对象的内部字段越多。|5|
        |添加参数|方法的执行的参数的取值满足该条件时才被抓取。示例：        -   示例方法：方法`createOrder`的源代码片段如下：

            ```
class User {
    private int userId;
    private String userName;
    private boolean isVIP;
    }
    public void createOrder(User user, String productId, double price)
            ```

        -   抓取条件：`userId`为8753的方法执行。
        -   参数设置：params\[0\].userId ; = ; 8753。
|params\[0\].userId ; = ; 8753|

    3.  单击![刷新](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8471964161/p245128.png)图标。

        方法页签下显示满足该抓取条件的某一次方法的执行信息。

5.  如需查看方法源码，在方法页签下，单击**查看方法源码**。

    如下图所示，每一次内部方法的执行耗时都会以注释的方式显示在源代码中。该方法的内部方法中执行耗时最高的方法的源代码标红显示。

    ![方法堆栈](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8471964161/p245129.png)


## 性能分析

性能分析支持对CPU耗时、内存分配等对象进行一定时间的采样并生成相应的火焰图，帮助您快速定位应用的性能瓶颈。

1.  在Arthas诊断页面，单击**性能分析**页签。

2.  在**性能分析**页签下方，单击**新建火焰图**。

3.  在**新建火焰图**对话框，选择火焰图类型，输入采样时间，输入备注信息，然后单击**确认**。

    |参数|描述|示例值|
    |--|--|---|
    |火焰图类型|采样对象的类型。取值：    -   cpu耗时
    -   内存分配
    -   锁耗时
    -   itimer
|cpu耗时|
    |输入采样时间\(单位：秒\)|采样的时长。取值：10~1800。|30|

    **性能分析**页签下方显示新建火焰图的任务信息，包括开始时间、采样时间、任务执行Pod等。

    ![性能分析](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7730864161/p245049.png)

4.  在**性能分析**页签下方，找到任务记录，在其右侧**任务状态**，单击**查看火焰图**，根据页面提示下载SVG格式的火焰图文件，然后在浏览器中打开。

    ![火焰图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7730864161/p245047.png)


