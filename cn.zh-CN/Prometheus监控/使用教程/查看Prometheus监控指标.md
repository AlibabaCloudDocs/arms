# 查看Prometheus监控指标

阿里云Prometheus监控提供的预置监控仪表板包括K8s集群概览、K8s部署、Pod和主机详情，您可以通过这些仪表板查看丰富的Prometheus监控指标，并按需更改仪表板数据的时间区间、刷新频率等属性。

[t855956.md\#section\_cpd\_cg9\_vul]()

## 打开监控仪表板

安装Prometheus监控插件后，即可在Prometheus监控页面打开预置的监控仪表板。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  单击**监控列表**，Prometheus监控页面会列出您的阿里云账号下在阿里云容器服务Kubernetes版中的全部Kubernetes集群。

4.  在Prometheus监控页面上，单击**已安装大盘**列中的链接，即可在浏览器新窗口中打开对应的监控仪表板。


## 查看监控指标

您可以通过以下预置监控仪表板查看监控指标。

-   K8s集群概览仪表板

    ![K8s Cluster Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p49438.png)

    该仪表板展示的监控指标主要包括：

    -   总体使用量信息：例如集群CPU使用率、集群内存使用率、集群文件系统使用率。
    -   CPU信息：例如Pod CPU使用率、全部进程CPU使用率。
    -   内存信息：例如Pod内存使用率、全部进程内存使用率。
    -   网络信息：例如网络I/O压力、Pod网络I/O、所有进程网络I/O。
-   K8s部署仪表板

    ![K8s Deployment Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51317.png)

    该仪表板展示的监控指标主要包括：

    -   概览：部署CPU使用率、部署内存使用率、不可用副本数。
    -   详情：CPU使用率、内存使用率、全部进程网络I/O。
-   Pod仪表板

    ![K8s Pods Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51318.png)

    该仪表板展示的监控指标主要包括：

    -   Pod基本信息：Pod IP地址、Pod状态、Pod容器、容器重启次数。
    -   总体使用量信息：例如Pod CPU使用率、Pod内存使用率。
    -   CPU信息：例如Pod CPU使用率、全部进程CPU使用率。
    -   内存信息：例如Pod内存使用率、全部进程内存使用率。
    -   网络信息：例如网络I/O压力、Pod网络I/O、所有进程网络I/O。
-   主机详情仪表板

    ![K8s Host Details Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p49437.png)

    该仪表板展示的监控指标主要包括：

    -   CPU信息：例如CPU核数、CPU使用率、CPU I/O等待时间。
    -   内存信息：例如内存总量、内存使用率。
    -   磁盘信息：例如磁盘总空间、磁盘IO读写时间、磁盘读写速率。
    -   网络信息：例如网络流量、TCP连接情况。

## 仪表板常用操作

对仪表板的常用操作如下所示。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51325.png)

1.  切换仪表板

    该下拉菜单显示当前查看的仪表板名称，并可用于切换至下拉菜单中的其他仪表板。您可以通过在顶部搜索栏中输入名称来查找仪表板，或者使用Filter（筛选条件）在下拉菜单中筛选出带有指定Tag（标签）的仪表板。

    ![Switch Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51327.png)

2.  设置时间区间和刷新频率

    单击此图标后，您可以在浮层中选择预定义的监控数据相对时间区间，例如过去5分钟、过去12小时、过去30天等，也可以通过设置时间起点和终点来设置自定义的绝对时间区间。此外，您可以在浮层中设置仪表板的刷新频率。

    ![Set Interval and Frequency](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51326.png)

3.  扩大时间区间

    每单击一次该扩大按钮，时间区间就会扩大为当前的两倍，且时间起点迁移和终点后移的幅度相等。例如，假设当前选择的时间区间为过去10分钟，则单击一次该过大按钮后，时间区间的前面和后面将会各延长5分钟。

4.  手动刷新

    单击此按钮将会刷新当前仪表板中所有面板的监控数据。

5.  筛选监控数据

    选择此下拉菜单中的选项即可筛选当前仪表板显示的监控数据。


## 仪表板面板常用操作

单击面板顶部的下拉菜单后，可进行以下操作：

![Panel Operation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5028986061/p51328.png)

-   全屏查看当前面板：单击**View**，或按快捷键V。再次按快捷键V或Esc即可退出全屏模式。
-   分享当前面板：单击**Share**，或依次按下P和S打开分享对话框，获得当前面板的分享链接、嵌入链接或快照链接。
-   获得当前面板的JSON代码：选择**More** \> **Panel JSON**，然后在JSON对话框中拷贝JSON代码。
-   将当前面板的数据导出为CSV文件：选择**More** \> **Export CSV**，然后在Export CSV对话框中设置导出格式并导出。
-   打开或关闭图例：选择**More** \> **Toggle legend**，或依次按下P和L即可切换图例的可见性。

[什么是Prometheus监控？]()

[t855956.md\#section\_cpd\_cg9\_vul]()

