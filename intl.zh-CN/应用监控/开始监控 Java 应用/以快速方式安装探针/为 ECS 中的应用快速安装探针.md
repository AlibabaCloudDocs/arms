# 为 ECS 中的应用快速安装探针 {#concept_109296_zh .concept}

借助 ARMS 应用监控，您可以对云服务器 ECS 上的应用进行应用拓扑、接口调用、异常事务和慢事务、SQL 分析等监控。ARMS 与 ECS 进行了数据联通，通过在 ARMS 控制台上简单操作即可快速为同阿里云账户下的 ECS 中的应用安装探针。

## 前提条件 {#section_zbs_pcj_ygb .section}

您已经在要部署应用的地域下[购买 ECS](https://ecs-buy.aliyun.com/)，并成功部署应用。

## 操作步骤 {#section_xqy_wdj_ygb .section}

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表** 。
2.  在应用列表页面右上角单击**新接入应用**。
3.  在新接入应用页面选择使用语言为 **Java**，选择使用环境为**云服务器 ECS**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360644390_zh-CN.png)

4.  首次接入时需要先进行 ARMS 访问 ECS 授权，请使用主账号完成授权。

    1.  在弹出的提示框中单击**进入 RAM 进行授权**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360643119_zh-CN.png)

    2.  在云资源访问授权页面选中 **AliyunARMSAccessingECSRole** 权限后单击**同意授权**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360643120_zh-CN.png)

    3.  在同步 ECS 页面单击**确定同步**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360646413_zh-CN.png)

    4.  关闭同步 ECS页面，完成授权。
    授权成功后，新接入应用页面中将显示此账号下所有 ECS 实例。

5.  在请选择您要安装探针的应用区域单击目标 ECS 实例**操作**列的**安装探针**，并在弹出的**提示**对话中单击**确认**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360643121_zh-CN.png)

    在 ECS 上安装探针成功后，ARMS 将获取此 ECS 上的所有进程信息并显示在目标 ECS 实例下方的进程列表中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360643122_zh-CN.png)

    **说明：** 若成功安装探针后，ECS 进程信息不准确，请单击 ECS 实例左侧的 **-** 号然后单击 **+** 号刷新信息。若探针安装失败请参见[常见问题](#section_wqk_sxc_zgb)进行处理。

6.  探针安装成功后，在下方的弹框中编辑目标进程的**应用名称**，然后单击**操作**列的**启用应用监控**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360743123_zh-CN.png)

    **说明：** 当多个进程的应用名称相同时，表现为一个监控任务下的多个实例。


约一分钟后，若您的应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载探针 {#section_l2f_wvc_zgb .section}

当您不需要监控 ECS 上的应用时，可以卸载 ECS 上的探针。卸载之后，ARMS 将停止对该 ECS 上所有应用的监控。操作步骤如下：

1.  在安装探针的 ECS 中执行 `jps -l` 命令查看所有进程，在执行结果中找到 `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` 对应的进程号。

    本示例中，对应的进程号为：62857。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152233/156750360743111_zh-CN.png)

2.  执行命令 `kill -9 进程号`。例如：`kill -9 62857`。

3.  重新启动您的应用。

## 常见问题 {#section_wqk_sxc_zgb .section}

探针安装失败怎么处理？

1.  确保您的 ECS 可以访问所在地域的探针下载链接。

    ``` {#codeblock_dx5_2od_kx8}
    首先确保 ECS 可以访问外网，且能够访问所在地域的探针下载链接。
    
    # 杭州地域
    http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh
    # 上海地域
    http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh
    # 青岛地域
    http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh
    # 北京地域
    http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh
    # 深圳地域
    http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh
    # 新加坡地域
    http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh           
    ```

2.  确保您的 ECS 可以访问 ARMS 控制台。

    ``` {#codeblock_0sv_mpl_lop}
    #国内
    https://arms.console.aliyun.com/
    
    #新加坡
    https://arms-ap-southeast-1.console.aliyun.com
    ```

3.  登录 [ECS 控制台](https://ecs.console.aliyun.com/#/home)，并完成以下检查工作。
    1.  在左侧导航栏中选择**运维与监控** \> **云助手**。
    2.  在云助手页面的搜索框中选择**命令名称**，并输入 InstallJavaAgent。

        若查找结果不存在，请联系 ARMS 钉钉服务账号 arms160804。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360743124_zh-CN.png)

    3.  在云助手页面的**执行记录**页签的搜索框中输入 `InstallJavaAgent` 命令对应的 ID，在查找结果中单击该记录右侧**操作**列的**查看结果**，查看 `InstallJavaAgent` 命令是否执行成功。若未执行成功，根据详细执行结果排查问题（如 ECS 磁盘满、未安装 Java Agent 等问题，可以通过清理磁盘或安装 Java Agent 解决），若不能解决请将详细执行结果反馈给 ARMS 钉钉服务账号 arms160804。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152235/156750360743125_zh-CN.png)


## 快速更改应用名称 {#section_k8u_2kh_k5n .section}

如果因为某些原因希望更改应用名称，例如忘记将示例应用名称 Java-Demo 修改为自定义名称，您可以在不重启应用、不重装探针的情况下更改应用名称，详情参见[部署在 ECS 中的 Java 应用（以快速方式安装探针时）](../../../../intl.zh-CN/常见问题/应用监控常见问题/如何在不重装探针的情况下更改 Java 应用名称？.md#section_zs3_iqg_tlj)。

## 相关文档 {#section_gr2_ds2_zgb .section}

 [为 ECS 中的应用快速安装探针的常见问题](../../../../intl.zh-CN/常见问题/应用监控常见问题/为 ECS 中的应用快速安装探针的常见问题.md#)

