# 管理 ECS 数据源 {#task_42906 .task}

ECS 实例是重要的日志产生来源，也是 ARMS 支持的自定义监控数据源。您可以授权 ARMS 将您阿里云账号下的 ECS 实例信息同步至 ARMS 控制台，为这些实例安装 Logtail 日志采集 Agent。您也可以为这些 ECS 实例分组以便管理。

执行同步 ECS 操作时必须使用阿里云账号或具备完整权限的 RAM 用户，不可使用不具备完整权限的 RAM 用户，例如仅具备只读权限的 RAM 用户。

## 同步 ECS 实例 {#section_r5m_28q_rrt .section}

为了进行后续的管理，首先需要将您阿里云账号下的 ECS 实例信息同步至 ARMS 控制台。

1.  2.  在左侧导航栏中选择**自定义监控数据源管理** \> **云服务器 ECS** 。
3.  在实例列表页面顶部选择目标地域，单击右上角的**同步ECS**。 

    **说明：** 同步操作仅针对当前所选地域。

    ![ECS Datasource Regions](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152292/156756993543559_zh-CN.png)

4.  如果您此前没有授权，则在提示框中单击**进入RAM进行授权**。 

    ![Dialog Box Authorize ARMS](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152292/156756993543560_zh-CN.png)

5.  在**云资源访问授权**页面选择所需权限，并单击**同意授权**。 

    ![Dialog Box Cloud Resource Authorization](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152292/156756993543561_zh-CN.png)

    **说明：** 如果您使用的是不具备完整权限的 RAM 子账号，则无法授权。请使用阿里云主账号或具备完整权限的 RAM 用户授权。


## 检查 Logtail Agent 状态 {#section_e1j_tpi_0tn .section}

ARMS 系统通过 Logtail（日志收集客户端）来收集 ECS 上的日志，因此您需要在每台 ECS 服务器上安装 Logtail。

您可以对单台 ECS 进行状态检查，也可以批量进行检查。

## 安装 Logtail Agent {#section_k4k_zpo_ym4 .section}

检测发现未安装 Agent 的机器，请参考[安装 Agent](intl.zh-CN/自定义监控/管理数据源/ECS 数据源/安装 Agent.md#)完成安装。

**说明：** ECS 安装完 Agent 之后，需要返回实例列表页面进行**检查 Agent** 操作，以更新当前 ECS 的相关状态。

