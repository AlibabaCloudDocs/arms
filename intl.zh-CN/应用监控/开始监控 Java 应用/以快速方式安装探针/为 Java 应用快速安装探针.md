# 为 Java 应用快速安装探针 {#concept_102784_zh .concept}

ARMS 提供一键接入方式为 Java 应用安装探针，操作简单，安装成功后无需重启应用即可开始监控，适用于新手用户。当应用重启时，探针会自动加载，该 Java 应用将自动接入 ARMS 应用监控。

## 前提条件 {#section_nsq_j5g_qgb .section}

-   确保您使用的第三方组件或框架在应用监控兼容性列表范围内，请参见[应用监控兼容性列表](intl.zh-CN/应用监控/参考信息/应用监控兼容性列表.md#)。

-   若您的应用已经按照手动接入方式接入 ARMS 应用监控，则需先卸载探针才能正常使用一键接入方式。请参见[卸载探针](intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为 Java 应用安装探针.md#uninstall)。

## 操作步骤 {#section_st2_rzl_lgb .section}

具体操作步骤如下：

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表** 。
2.  在应用列表页面右上角单击**新接入应用**。
3.  在新接入应用页面选择使用语言为 **Java**，选择使用环境为**默认环境**，选择接入方式为**一键接入**。 然后查看并保存 LicenseKey。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152233/156741139944367_zh-CN.png)

4.  运行您所在地域对应的安装脚本。

    -   将 `<licenseKey>` 替换为您的 LicenseKey。

    -   将 `Java-Demo` 替换成您的应用名，应用名暂不支持中文。

    ``` {#codeblock_e0k_zh6_8rv}
    # 杭州地域
    wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 上海地域
    wget -O- http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 青岛地域
    wget -O- http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 北京地域
    wget -O- http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 深圳地域
    wget -O- http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 新加坡地域
    wget -O- http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # 金融云环境
    wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ```


**说明：** 

-   执行安装脚本后，该脚本会自动下载最新探针。
-   若您的服务器只有一个 Java 进程，安装脚本会默认选择该进程安装探针；若您的服务器有多个 Java 进程，请根据提示选择一个进程安装探针。

## 结果验证 {#section_w1t_4ca_kti .section}

约一分钟后，若您的应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载探针 {#section_xkw_j3m_lgb .section}

当您不需要 ARMS 探针采集数据时，可按照以下步骤卸载探针。

1.  执行 `jps -l` 命令，并在执行结果中找到 `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` 对应的进程号。

    在本示例中，`com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` 对应的进程号为：62857。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152233/156741140043111_zh-CN.png)

2.  执行命令 `kill -9 进程号`。例如：`kill -9 62857`。
3.  重新启动您的应用。

## 快速更改应用名称 {#section_hot_ot1_6hw .section}

如果因为某些原因希望更改应用名称，例如忘记将示例应用名称 Java-Demo 修改为自定义名称，您可以在不重启应用、不重装探针的情况下更改应用名称，详情参见[普通 Java 应用（以快速方式安装探针时）](../../../../intl.zh-CN/常见问题/应用监控常见问题/如何在不重装探针的情况下更改 Java 应用名称？.md#section_j8u_9a8_b5t)。

## 常见问题 {#section_cpz_bwg_qgb .section}

1.  如果在执行一键接入 Java 应用脚本时出现以下 getcwd 相关错误该怎么处理？

    ``` {#codeblock_i3b_z7v_5k2}
    shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory Error occurred during initialization of VM java.lang.Error: Properties init: Could not determine current working directory. at java.lang.System.initProperties(Native Method) at java.lang.System.initializeSystemClass(System.java:1119)
    ```

    可能原因是执行脚本过程中误删了当前目录。解决办法为：先执行 `cd`，然后重新运行脚本。

2.  使用一键接入方式安装探针后，在哪里查看日志？

    日志的默认目录为：/root/.arms/supervisor/logs/arms-supervisor.log，若此目录下没有日志，请执行命令`ps -ef |grep arms`查看日志所在目录。


## 更多信息 {#section_d4p_2y1_mgb .section}

-   [为 Java 应用安装探针的常见问题](../../../../intl.zh-CN/常见问题/应用监控常见问题/为 Java 应用安装探针的常见问题.md#)
-   [使用 OpenFeign 组件的应用在 ARMS 中数据不完整怎么办？](../../../../intl.zh-CN/常见问题/应用监控常见问题/使用 OpenFeign 组件的应用在 ARMS 中数据不完整怎么办？.md#)
-   [为 Java 应用快速安装探针的常见问题](../../../../intl.zh-CN/常见问题/应用监控常见问题/为 Java 应用快速安装探针的常见问题.md#)

