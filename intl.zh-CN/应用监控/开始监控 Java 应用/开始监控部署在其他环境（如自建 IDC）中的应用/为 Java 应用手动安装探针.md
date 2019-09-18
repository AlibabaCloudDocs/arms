# 为 Java 应用手动安装探针 {#concept_63797_zh .concept}

为 Java 应用安装 ARMS 探针后，ARMS 即可对 Java 应用进行应用拓扑、调用链路追踪、异常事务和慢事务监控、SQL 分析等一系列监控。安装探针可采用手动接入方式和一键接入方式。本文将介绍如何为 Java 应用手动安装探针。

## 前提条件 {#section_rgl_qs1_mgb .section}

-   确保您使用的公网服务器安全组已开放 8442、8443、8883 三个端口的 TCP 公网出方向权限，VPC 内不需要开通。为阿里云 ECS 开放出方向权限，请参见[添加安全组规则](../../../../intl.zh-CN/安全/安全组/添加安全组规则.md#)。

    **说明：** ARMS 不仅可接入阿里云 ECS 上的应用，还能接入其他能访问公网的服务器上的应用。

-   确保您使用的第三方组件或框架在应用监控兼容性列表范围内，请参见[应用监控兼容性列表](intl.zh-CN/应用监控/参考信息/应用组件和框架支持列表.md#)。


## 操作步骤 {#step1 .section}

为 Java 应用安装探针操作步骤如下：

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表** 。
2.  在应用列表页面右上角单击**新接入应用**。

3.  在新应用接入页面选择使用语言为 **Java**，选择使用环境为**默认**，选择接入方式为**手动接入**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152228/156879648144353_zh-CN.png)

4.  采用以下方法之一下载探针，然后在控制台下载探针页签中单击**下一步**。

    -   方法一：手动下载。在下载探针页签中单击**下载探针**按钮，下载最新 ZIP 包。

    -   方法二：Wget 命令下载。根据您的地域使用 Wget 命令下载对应的探针压缩包。

    ``` {#codeblock_fi0_fsx_erz}
    # 杭州地域
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 上海地域
    wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 青岛地域
    wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 北京地域
    wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 张家口地域
    wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 深圳地域
    wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    # 新加坡地域
    wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
    # 金融云环境
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
    ```

5.  切换到探针安装包所在目录，并执行以下命令解压安装包到任意工作目录下。

    **说明：** \{user.workspace\} 是示例目录。

    ``` {#codeblock_k9l_l7g_a75}
    unzip ArmsAgent.zip -d /{user.workspace}/ 
    ```

6.  在控制台安装探针页签中查看并保存 LicenseKey。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152228/156879648142270_zh-CN.png)

7.  采用以下方法之一添加 AppName 以及 LicenseKey 参数。

    -   方法一：根据您的应用运行环境修改 JVM 参数。

        **说明：** 将 `<LicenseKey>` 替换成您的 LicenseKey；将 `<AppName>` 替换成您的应用名称，应用名暂不支持中文；将\{user.workspace\} 替换成实际探针解压的目录。

        -   Tomcat 运行环境

            -   在 Linux 或 Mac 环境下，请在 \{TOMCAT\_HOME\}/bin 目录下的 setenv.sh 文件中加入以下配置。

                **说明：** 

                如果您的 Tomcat 版本没有 setenv.sh 配置文件，请打开 \{TOMCAT\_HOME\}/bin/catalina.sh 文件，找到 `JAVA_OPTS` 变量定义，并在该变量定义后加入以下配置。

                **点击下载参考样例：**[catalina.sh](https://arms-public.oss-cn-shanghai.aliyuncs.com/arms-agent/catalina.sh)（第 256 行定义）。

                ``` {#codeblock_v8h_2h6_onw}
                JAVA_OPTS="$JAVA_OPTS -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName>" 
                ```

            -   在 Windows 环境下，请在 \{TOMCAT\_HOME\}/bin/catalina.bat 文件中加入以下配置：

                ``` {#codeblock_igo_h7w_jn5}
                set "JAVA_OPTS=%JAVA_OPTS% -javaagent:{user.workspace}ArmsAgentarms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName>" 
                ```

        -   Jetty 运行环境

            在 \{JETTY\_HOME\}/start.ini 配置文件中加入以下配置：

            ``` {#codeblock_9si_bg2_dfe}
            --exec #打开注释 前面的井号去掉即可 -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> 
            ```

        -   Spring Boot 运行环境

            启动 Spring Boot 进程时，在启动命令后面加上 -javaagent 参数：

            ``` {#codeblock_afo_55h_w8u}
            java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> -jar demoApp.jar 
            ```

            **说明：** demoApp.jar 为原应用 JAR 包名称，请根据实际情况替换。

        -   Resin 运行环境

            1.  启动 Resin 进程时，需要在 conf/resion.xml 配置文件中添加以下标签：

                ``` {#codeblock_7pu_x7k_q2m}
                <server-default> <jvm-arg>-javaagent:{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar</jvm-arg> <jvm-arg>-Darms.licenseKey=<LicenseKey> </jvm-arg> <jvm-arg>-Darms.appName=<AppName> </jvm-xxxarg> </server-default> 
                ```

            2.  在 conf/app-default.xml 文件中添加以下标签：

                ``` {#codeblock_kvd_jc7_bq5}
                <library-loader path="{user.workspace}/ArmsAgent/plugin"/> 
                ```

        -   Windows 运行环境

            在 Windows 环境下启动 Java 进程时，请在挂载探针路径中使用反斜杠作为分隔符。

            ``` {#codeblock_crd_tly_swi}
            {CMD}> java -javaagent:{user.workspace}ArmsAgentarms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> -jar {user.workspace}demoApp.jar 
            ```

            **说明：** demoApp.jar 为原应用 JAR 包名称，请根据实际情况替换。

        同一台机器上面，部署同一应用的多个实例场景，可以通过 -Darms.agentId（逻辑编号：如 001，002）参数来区分接入的 JVM 进程，例如：

        ``` {#codeblock_d4i_jju_vot}
            java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> 
            -Darms.agentId=001 -jar demoApp.jar
        ```

    -   方法二：

        1.  修改 arms-agent.config 文件。将 <LicenseKey\> 替换成您的 LicenseKey；将 <AppName\> 替换成您的应用名称，应用名暂不支持中文字符。

            ``` {#codeblock_k8g_iib_1ew}
            arms.licenseKey=<LicenseKey> arms.appName=<AppName>
            ```

        2.  修改 JVM 参数，在 Java 应用的启动脚本中添加以下参数。

            ``` {#codeblock_f01_ib9_cjt}
            -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar 
            ```

            **说明：** 将 \{user.workspace\} 替换成实际探针解压的目录。

8.  重启 Java 应用。


## 结果验证 {#section_4d8_ffi_d65 .section}

约一分钟后，若 Java 应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载 Java 探针 {#uninstall .section}

1.  删除[第 7 步](#codeph_mzu_zln_tg7)中添加的 AppName、LicenseKey 相关的所有参数。
2.  重启 Java 应用。

## 快速更改应用名称 {#section_4og_31l_fqp .section}

如果因为某些原因希望更改应用名称，例如忘记将示例应用名称 Java-Demo 修改为自定义名称，您可以在不重启应用、不重装探针的情况下更改应用名称，详情参见[普通 Java 应用（以普通方式安装探针时）](../../../../intl.zh-CN/常见问题/应用监控常见问题/如何在不重装探针的情况下更改 Java 应用名称？.md#section_czl_pxe_z9v)。

## 相关文档 {#section_d4p_2y1_mgb .section}

-   [为 Java 应用安装探针的常见问题](../../../../intl.zh-CN/常见问题/应用监控常见问题/为 Java 应用安装探针的常见问题.md#)
-   [使用 OpenFeign 组件的应用在 ARMS 中数据不完整怎么办？](../../../../intl.zh-CN/常见问题/应用监控常见问题/使用 OpenFeign 组件的应用在 ARMS 中数据不完整怎么办？.md#)

