# 如何在不重装探针的情况下更改 Java 应用名称？ {#task_1846738 .task}

使用 ARMS 监控 Java 应用时，如果因为某些原因希望更改应用名称，例如忘记将示例应用名称 Java-Demo 修改为自定义名称，您可以按照本文的说明，在不重启应用、不重装探针的情况下更改应用名称。

探针版本为 2.5.8.1 或以上。您可以在探针目录的 Version 文件中查看探针版本。例如，`2.5.8_cf020486_20190816150025` 表示探针版本为 2.5.8，探针发布时间为 2019 年 8 月 16 日。探针目录的位置因安装探针的方式而异，详见以下内容。

## 普通 Java 应用（以普通方式安装探针时） {#section_czl_pxe_z9v .section}

普通 Java 应用是指除了部署在阿里云 ECS 实例上的 Java 应用之外的应用。如果您是以普通方式安装探针的，则探针目录就是您自定义的位置。

请按照以下步骤更改应用名称。

1.  请使用以下方法之一下载并解压 Supervisor。 

    **说明：** 请根据您的应用所在的地域替换下载地址中的地域。

    -   公网地址

        ``` {#codeblock_9r4_bjg_ae6}
        wget http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsSupervisor.zip -O ArmsSupervisor.zip
        unzip ArmsSupervisor.zip
        ```

    -   VPC 地址（公网地址无法下载时使用）

        ``` {#codeblock_nm0_ifp_nks}
        wget http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/ArmsSupervisor.zip -O ArmsSupervisor.zip
        unzip ArmsSupervisor.zip
        ```

2.  运行以下命令更改应用名称。 

    ``` {#codeblock_3y4_krx_nk3}
    cd ArmsSupervisor
    ./attach.sh </path/to/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar> <PID> <NewAppName> <LicenseKey>
    ```

    -   </path/to/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar\>：指向探针下同名文件的路径。
    -   <PID\>：目标进程 ID，可通过 `jps/ps` 命令获取。
    -   <NewAppName\>：新的应用名称。
    -   <LicenseKey\>：ARMS 应用监控中应用的 LicenseKey，可从控制台获取。

如果应用的标准输出打印以下日志，则说明应用名称更改成功。

![Name Change Success](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1463780/156680779957403_zh-CN.png)

## 普通 Java 应用（以快速方式安装探针时） {#section_j8u_9a8_b5t .section}

如果您是以快速方式安装探针的，则探针目录为 ~/.arms/supervisor/agent。注意，使用的账号必须与应用相同。

请按照以下步骤更改应用名称。

1.  登录应用所在的机器，并运行以下命令。 

    ``` {#codeblock_gdj_x4d_xw9}
    cd ~/.arms/supervisor
    ./cli.sh <LicenseKey> <NewAppName>
    ```

    -   <LicenseKey\>：ARMS 应用监控中应用的 LicenseKey，可从控制台获取。
    -   <NewAppName\>：新的应用名称。
2.  从程序列出的所有 Java 进程中选择正确的进程。 

    **说明：** 如果只有一个应用进程则默认选中该进程。

3.  打开 ~/.arms/attach.info 文件，将需要修改的旧应用名称修改为新应用名称并保存文件。 

    **警告：** 修改文件时切勿多加空格等内容。


如果应用的标准输出打印以下日志，则说明应用名称更改成功。

![Name Change Success](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1463780/156680779957403_zh-CN.png)

## 部署在 ECS 中的 Java 应用（以快速方式安装探针时） {#section_zs3_iqg_tlj .section}

如果是部署在 ECS 实例中的 Java 应用，则探针目录为 /.arms/agent。

请按照以下步骤更改应用名称。

1.  登录应用所在的机器，并使用 root 账号运行以下命令。 

    ``` {#codeblock_2b2_e18_dro}
    su <USER> -c "./attach.sh /.arms/agent/arms-bootstrap-1.7.0-SNAPSHOT.jar <PID> <NewAppName> <LicenseKey>"
    ```

    -   <PID\>：目标进程 ID，可通过 `jps/ps` 命令获取。
    -   <NewAppName\>：新的应用名称。
    -   <LicenseKey\>：ARMS 应用监控中应用的 LicenseKey，可从控制台获取。
2.  打开 ~/.arms/attach.info 文件，将需要修改的旧应用名称修改为新应用名称并保存文件。 

    **警告：** 修改文件时切勿多加空格等内容。


如果应用的标准输出打印以下日志，则说明应用名称更改成功。

![Name Change Success](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1463780/156680779957403_zh-CN.png)

## 部署在容器服务 K8s 集群中的 Java 应用 {#section_iw6_l4v_c66 .section}

如果是部署在容器服务 K8s 集群中的 Java 应用，修改 Deployment 内的 armsPilotCreateAppName 参数并重启 Pod 即可。

## 部署在 EDAS 上的 Java 应用 {#section_25m_0la_1y1 .section}

目前无法为部署在 EDAS 上的 Java 应用更改应用名称。

应用名称更改成功后稍等片刻，旧名称的应用下将不再有监控数据上报，且新名称的应用下将有监控数据上报。

[为 Java 应用安装探针](../../../../intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为 Java 应用安装探针.md#)

[为 Java 应用快速安装探针](../../../../intl.zh-CN/应用监控/开始监控 Java 应用/以快速方式安装探针/为 Java 应用快速安装探针.md#)

[为 ECS 中的应用快速安装探针](../../../../intl.zh-CN/应用监控/开始监控 Java 应用/以快速方式安装探针/为 ECS 中的应用快速安装探针.md#)

[为容器服务 Kubernetes 版 Java 应用安装探针](../../../../intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为容器服务 Kubernetes 版 Java 应用安装探针.md#)

