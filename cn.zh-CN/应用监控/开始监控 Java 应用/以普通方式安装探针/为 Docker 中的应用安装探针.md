# 为 Docker 中的应用安装探针 {#concept_85906_zh .concept}

为 Docker 中的 Java 应用安装 ARMS 探针后，ARMS 即可对该应用进行应用拓扑、调用链路追踪、异常事务和慢事务监控、SQL 分析等一系列监控。

## 背景信息 {#section_gxt_gtr_xk4 .section}

[Docker](https://docs.docker.com/) 是一个开放源代码软件项目，让应用程序部署在软件货柜下的工作可以自动化进行，借此在Linux操作系统上，提供一个额外的软件抽象层，以及操作系统层虚拟化的自动管理机制。 Docker利用 Linux 核心中的资源分离机制，例如 cgroups，以及 Linux 核心名字空间，来创建独立的容器。

为 Docker 中的应用安装 ARMS 探针后，ARMS 将自动适配该应用运行的环境，不需要针对 Tomcat、Jetty 和 Springboot 等应用配置运行环境。

## 前提条件 {#section_c31_apg_k5z .section}

1.  您已成功开通 ARMS 服务，请参见[开通 ARMS](../intl.zh-CN/快速入门/开通 ARMS.md#)。

2.  您已在 Docker 中部署 Java 应用。

## 操作步骤 {#section_trt_vzp_n2b .section}

如果有一个已部署 Java 应用的镜像 \{original-docker-image:tag\}，可以通过编辑 Dockerfile 文件集成已有镜像来形成新的镜像，然后构建、启动新的镜像即可将 Java 应用接入 ARMS 应用监控。具体操作步骤如下：

1.  通过编辑 Dockerfile 集成 \{original-docker-image:tag\} 镜像。Dockerfile 示例如下：

    ``` {#codeblock_f4g_bz4_jhu}
    ###################################
    ##                              ###
    ##      ARMS APM DEMO Docker    ###
    ##          For Java            ###
    ##      withAgent   V0.1        ###
    ##                              ###
    ###################################
    FROM {original-docker-image:tag}
    WORKDIR /root/
    # 请根据所在地域替换探针的下载地址。
    RUN wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    RUN unzip ArmsAgent.zip -d /root/
    # LicenseKey 在控制台应用监控接入页面查看。
    # AppName 为用户自定义 ARMS 监控应用名称，用户名暂不支持中文。
    # 若所有镜像都接入同一个应用监控任务，配置此处的 arms_licenseKey 和 arms_appName 即可。
    # 若需将镜像接入其他应用监控任务，可在 docker run 中使用 -e 参数指定该应用的 arms_licenseKey 和 arms_appName 参数，以覆盖此处的配置。
    ENV arms_licenseKey=xxx
    ENV arms_appName=xxx
    ENV JAVA_TOOL_OPTIONS ${JAVA_TOOL_OPTIONS} '-javaagent:/root/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey='${arms_licenseKey}' -Darms.appName='${arms_appName}
    ### for check the args
    RUN env | grep JAVA_TOOL_OPTIONS
    ### 下面可加入用户 自定义 dockerfile 逻辑。
    ### ......
    ```

    -   将配置中的 `original-docker-image:tag` 替换为您自己的镜像地址。若您没有自定义镜像，可使用系统镜像。
    -   根据所在地域替换探针的下载地址。

        ``` {#codeblock_lna_67l_4wk}
        # 杭州地域
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # 上海地域
        wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # 青岛地域
        wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # 北京地域
        wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # 深圳地域
        wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # 新加坡地域
        wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
        # 金融云环境
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip`
        ```

    -   将 `arms_licenseKey` 和 `arms_appName` 分别替换成您的 LicenseKey 和应用名称。获取 LicenseKey 步骤如下：
        1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
        2.  在应用列表页面右上角单击**新接入应用**。
        3.  在新接入应用页面顶部单击 License Key 右侧的复制图标。

            ![Section LicenseKey](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152532/156741482045312_zh-CN.png)

2.  运行 docker build 命令来构建镜像。示例如下：

    ``` {#codeblock_x45_66y_9mu}
    docker build -t registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1 -f /{workspace}/Dockerfile /{workspace}/
    ```

    **说明：** `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1` 为镜像名称，请根据实际修改。

3.  运行 docker run 命令来启动镜像。

    使用原有镜像 \{original-docker-image:tag\}的 docker run 启动脚本来启动即可。若需将镜像接入其他应用监控任务，可在 docker run 中使用 `-e` 参数指定该应用的 `arms_licenseKey` 和 `arms_appName` 参数，以覆盖 Dockerfile 中的配置。示例如下：

    ``` {#codeblock_jo7_sk0_2lw}
    docker run -d -e "arms_licenseKey=<LicenseKey>" -e "arms_appName=<AppName>" -p 8081:8080 registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1
    ```

    **说明：** 

    -   将 `<LicenseKey>`替换成您的 LicenseKey，将`<AppName>`替换成您的应用名称，应用名暂不支持中文。
    -   `registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1` 为镜像名称，请根据实际修改。

## 结果验证 {#section_x7u_dja_3ds .section}

约一分钟后，若您的应用出现在应用列表中且有数据上报，则说明接入成功。

