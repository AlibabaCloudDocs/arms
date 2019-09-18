# 查看 Prometheus 监控指标 {#task_124815_zh .task}

ARMS Prometheus 监控提供的预置监控仪表板包括 K8s 集群概览、K8s 部署、Pod 和主机详情，您可以通过这些仪表板查看丰富的 Prometheus 监控指标，并按需更改仪表板数据的时间区间、刷新频率等属性。

[安装 Prometheus 监控插件](intl.zh-CN/Prometheus 监控/开始使用 Prometheus 监控.md#section_cpd_cg9_vul)

## 打开监控仪表板 {#section_qdw_g0g_gg7 .section}

安装 Prometheus 监控插件后，即可在 Prometheus 监控页面打开预置的监控仪表板。

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。
2.  在左侧导航栏中单击 **Prometheus 监控**。 Prometheus 监控页面会列出您的阿里云账号下在阿里云容器服务 Kubernetes 版中的全部 Kubernetes 集群。
3.  在 Prometheus 监控页面上，单击**已安装插件**列中的链接，即可在浏览器新窗口中打开对应的监控仪表板。

## 查看监控指标 {#section_q5z_yb5_1f6 .section}

您可以通过以下预置监控仪表板查看监控指标。

-   K8s 集群概览仪表板

    ![K8s Cluster Overview](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/531966/156880475449438_zh-CN.png)

    该仪表板展示的监控指标主要包括：

    -   总体使用量信息：例如集群 CPU 使用率、集群内存使用率、集群文件系统使用率。
    -   CPU 信息：例如 Pod CPU 使用率、全部进程 CPU 使用率。
    -   内存信息：例如 Pod 内存使用率、全部进程内存使用率。
    -   网络信息：例如网络 I/O 压力、Pod 网络 I/O、所有进程网络 I/O。
-   K8s 部署仪表板

    ![K8s Deployment Dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451317_zh-CN.png)

    该仪表板展示的监控指标主要包括：

    -   概览：部署 CPU 使用率、部署内存使用率、不可用副本数。
    -   详情：CPU 使用率、内存使用率、全部进程网络 I/O。
-   Pod 仪表板

    ![K8s Pods Dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451318_zh-CN.png)

    该仪表板展示的监控指标主要包括：

    -   Pod 基本信息：Pod IP 地址、Pod 状态、Pod 容器、容器重启次数。
    -   总体使用量信息：例如 Pod CPU 使用率、Pod 内存使用率。
    -   CPU 信息：例如 Pod CPU 使用率、全部进程 CPU 使用率。
    -   内存信息：例如 Pod 内存使用率、全部进程内存使用率。
    -   网络信息：例如网络 I/O 压力、Pod 网络 I/O、所有进程网络 I/O。
-   主机详情仪表板

    ![K8s Host Details Dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/531966/156880475449437_zh-CN.png)

    该仪表板展示的监控指标主要包括：

    -   CPU 信息：例如 CPU 核数、CPU 使用率、CPU I/O 等待时间。
    -   内存信息：例如内存总量、内存使用率。
    -   磁盘信息：例如磁盘总空间、磁盘 IO 读写时间、磁盘读写速率。
    -   网络信息：例如网络流量、TCP 连接情况。

## 仪表板常用操作 {#section_vqz_wfd_18o .section}

对仪表板的常用操作如下所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451325_zh-CN.png)

1.  切换仪表板

    该下拉菜单显示当前查看的仪表板名称，并可用于切换至下拉菜单中的其他仪表板。您可以通过在顶部搜索栏中输入名称来查找仪表板，或者使用 Filter（筛选条件）在下拉菜单中筛选出带有指定 Tag（标签）的仪表板。

    ![Switch Dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451327_zh-CN.png)

2.  设置时间区间和刷新频率

    单击此图标后，您可以在浮层中选择预定义的监控数据相对时间区间，例如过去 5 分钟、过去 12 小时、过去 30 天等，也可以通过设置时间起点和终点来设置自定义的绝对时间区间。此外，您可以在浮层中设置仪表板的刷新频率。

    ![Set Interval and Frequency](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451326_zh-CN.png)

3.  扩大时间区间

    每单击一次该扩大按钮，时间区间就会扩大为当前的两倍，且时间起点迁移和终点后移的幅度相等。例如，假设当前选择的时间区间为过去 10 分钟，则单击一次该过大按钮后，时间区间的前面和后面将会各延长 5 分钟。

4.  手动刷新

    单击此按钮将会刷新当前仪表板中所有面板的监控数据。

5.  筛选监控数据

    选择此下拉菜单中的选项即可筛选当前仪表板显示的监控数据。


## 仪表板面板常用操作 {#section_qzo_6a1_jgc .section}

单击面板顶部的下拉菜单后，可进行以下操作：

![Panel Operation](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868729/156880475451328_zh-CN.png)

-   全屏查看当前面板：单击 **View**，或按快捷键 V。再次按快捷键 V 或 Esc 即可退出全屏模式。
-   分享当前面板：单击 **Share**，或依次按下 P 和 S 打开分享对话框，获得当前面板的分享链接、嵌入链接或快照链接。
-   获得当前面板的 JSON 代码：选择 **More** \> **Panel JSON**，然后在 JSON 对话框中拷贝 JSON 代码。
-   将当前面板的数据导出为 CSV 文件：选择 **More** \> **Export CSV**，然后在 Export CSV 对话框中设置导出格式并导出。
-   打开或关闭图例：选择 **More** \> **Toggle legend**，或依次按下 P 和 L 即可切换图例的可见性。

[Prometheus 监控概述](intl.zh-CN/Prometheus 监控/Prometheus 监控概述.md#)

[安装 Prometheus 监控插件](intl.zh-CN/Prometheus 监控/开始使用 Prometheus 监控.md#section_cpd_cg9_vul)

