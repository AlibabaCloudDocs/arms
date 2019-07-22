# 如何更新应用监控 Java 探针版本？ {#concept_1305370 .concept}

对于在 ARMS 中监控的 EDAS 应用、容器服务应用和其他类型应用，请按照本文所述的相应方法更新 Java 探针版本。

## 如何为 EDAS 应用更新探针？ {#section_eb1_d7z_762 .section}

要为 EDAS 应用更新 Java 探针版本，重新部署 EDAS 应用即可。

## 如何为容器服务应用更新探针？ {#section_xoa_mp5_j4v .section}

要为容器服务应用更新 Java 探针版本，重启 Pod 即可。

## 如何为其他类型的应用更新探针？ {#section_sz3_odg_foz .section}

要为除了 EDAS 应用和容器服务应用之外的其他类型应用更新 Java 探针版本，先卸载探针再重新安装即可。

如需卸载探针，请根据情况按照以下步骤操作：

-   为 ECS 应用卸载 Java 探针

    1.  在安装探针的 ECS 中执行 `jps -l` 命令查看所有进程，在执行结果中找到 `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` 对应的进程号。

        本示例中，对应的进程号为：62857。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152233/156376370143111_zh-CN.png)

    2.  执行命令 `kill -9 进程号`。例如：`kill -9 62857`。

    3.  重新启动您的应用。
-   为其他类型应用卸载 Java 探针

    请删除在配置文件或启动脚本中添加的 AppName、LicenseKey 相关参数。具体方法参见[卸载 Java 探针](../intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为 Java 应用安装探针.md#uninstall)。


