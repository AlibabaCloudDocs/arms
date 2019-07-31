# 为容器服务 Kubernetes 版 PHP 应用安装探针 {#arms_cs_k8s_php .task}

只需安装 ARMS 应用监控组件（探针），即可对部署在容器服务 Kubernetes 版中的 PHP 应用进行监控，查看应用拓扑、接口调用、异常事务和慢事务等方面的监控数据。本文介绍如何为容器服务 Kubernetes 版 PHP 应用安装探针。

-   [创建Kubernetes 集群](../../../../../intl.zh-CN/用户指南/Kubernetes集群/集群管理/创建Kubernetes 集群.md#)
-   [创建命名空间](../../../../../intl.zh-CN/Kubernetes集群用户指南/命名空间管理/创建命名空间.md#)：本文示例中的命名空间名称为 arms-demo

## 安装 ARMS 应用监控组件 {#section_9xu_c60_25t .section}

首先需要安装 ARMS 应用监控组件 ack-arms-pilot。

1.  登录[容器服务 Kubernetes 版控制台](https://cs.console.aliyun.com/#/k8s/overview)。
2.  在左侧导航栏选择**市场** \> **应用目录**，在右侧选中 **ack-arms-pilot**。
3.  在应用目录 - ack-arms-pilot 页面上，在右侧的创建面板中选择前提条件中创建的集群和命名空间，并单击**创建**。

## 为容器服务 Kubernetes 版授权 {#section_5i7_3vc_qu5 .section}

接下来要为容器服务 Kubernetes 版授予 ARMS 资源的访问权限。

1.  使用主账号登录[容器服务 Kubernetes 版控制台](https://cs.console.aliyun.com/#/k8s/overview)。
2.  在左侧导航栏选择**集群** \> **集群**，在目标集群右侧**操作**列单击**管理**。 

    ![Manage Cluster](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156454842053701_zh-CN.png)

3.  在目标集群的基本信息页面上，单击**集群资源**区域的 Worker RAM 角色链接。 

    ![Worker RAM Link](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156454842053704_zh-CN.png)

4.  在 RAM 访问控制控制台的 RAM 角色管理页面上，单击**权限管理**页签上的目标权限策略名称链接。
5.  在**策略内容**页签上单击**修改策略内容**，并在右侧的修改策略内容面板将以下内容添加到**策略内容**中，最后单击**确认**。 

    ``` {#d7e144}
    {
       "Action": "arms:*",
       "Resource": "*",
       "Effect": "Allow"
    }
    ```

    ![Modify RAM Authorization](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156454842053703_zh-CN.png)


## 为 PHP 应用开启 ARMS 应用监控 {#section_qfx_dbs_xcf .section}

以下步骤分别对应创建新应用和已有应用这两种情况。

如需在创建新应用的同时开启 ARMS 应用监控，请按以下步骤操作。

1.  在容器服务管理控制台左侧导航栏选择**应用** \> **无状态**
2.  在无状态（Deployment）页面右上角单击 **使用模板创建**。
3.  在使用模板创建页面上选择 **集群**、 **命名空间**和 **示例模板**，并在 **模板**（YAML 格式）中将以下 `annotations` 添加到 spec \> template \> metadata 层级下。 

    **说明：** 请将 <your-deployment-name\> 替换为您的应用名称。

    ``` {#d7e380}
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"
      armsAppType: PHP                                
    ```

4.  （本步骤仅限首次安装时）请修改 arms-pilot 安装的同名命名空间下的 ConfigMap arms-php.ini，该文件内容为 php.ini 默认配置。 

    **说明：** 注意修改 extension=/usr/local/arms/arms-php-agent/arms-7.2.so，arms-7.2.so 中的 7.2 为您的 PHP 版本，可使用的值为 5.4/5.5/5.6/7.0/7.1/7.2。

5.  挂载 arms-php.ini ConfigMap 项到 php.ini 文件 spec \> template \> spec \> containers 下，将 mountPath 设置为您的 php.ini 文件路径。 

    ``` {#d7e429}
    volumeMounts:
            - name: php-ini
              mountPath: /etc/php/7.2/fpm/php.ini
              subPath: php.ini
    ```

    ``` {#d7e432}
    volumes:
          - name: php-ini
            configMap:
              name: arms-php.ini
    ```

    创建一个无状态（Deployment）应用并开启 ARMS 应用监控的完整 YAML 示例模板如下：


如需为现有应用开启 ARMS 应用监控，请按以下步骤操作。

1.  在容器服务管理控制台左侧导航栏选择**应用** \> **无状态**或**应用** \> **有状态**。
2.  在无状态（Deployment）或有状态（StatefulSet）页面上，选择 **集群**和 **命名空间**，并在目标应用右侧 **操作**列中选择**更多** \> **查看 Yaml**。
3.  在编辑 YAML 对话框中将以下 `annotations` 添加到 spec \> template \> metadata 层级下，并单击 **更新**。 

    **说明：** 请将 <your-deployment-name\> 替换为您的应用名称。

    ``` {#d7e519}
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"
      armsAppType: PHP                                
    ```

4.  挂载 arms-php.ini ConfigMap 项到 php.ini 文件 spec \> template \> spec \> containers 下，将 mountPath 设置为您的 php.ini 文件路径。 

    ``` {#d7e545}
    volumeMounts:
            - name: php-ini
              mountPath: /etc/php/7.2/fpm/php.ini
              subPath: php.ini
    ```

    ``` {#d7e548}
    volumes:
          - name: php-ini
            configMap:
              name: arms-php.ini
    ```


在无状态（Deployment）或有状态（StatefulSet）页面上，目标应用的**操作**列将出现 **ARMS 控制台**按钮。

![ARMS Console Button](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1135134/156454842053712_zh-CN.png)

**说明：** 若**操作**列没有出现 **ARMS 控制台**，请检查您是否已授权容器服务访问 ARMS 资源。

[创建Kubernetes 集群](../../../../../intl.zh-CN/用户指南/Kubernetes集群/集群管理/创建Kubernetes 集群.md#)

[创建命名空间](../../../../../intl.zh-CN/Kubernetes集群用户指南/命名空间管理/创建命名空间.md#)

[为容器服务 Kubernetes 版 Java 应用安装探针](intl.zh-CN/应用监控/开始监控 Java 应用/以普通方式安装探针/为容器服务 Kubernetes 版 Java 应用安装探针.md#)

