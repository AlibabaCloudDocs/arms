---
keyword: [PHP, 应用监控, 容器服务]
---

# 为容器服务Kubernetes版PHP应用安装Agent

为部署在容器服务Kubernetes版中的PHP应用安装ARMS PHP Agent后，ARMS即可开始监控PHP应用，您可以查看应用拓扑、调用链路、异常事务、慢事务和SQL分析等一系列监控数据。本文介绍如何为容器服务Kubernetes版PHP应用安装Agent。

## 步骤一：获取应用监控License Key

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

3.  在应用列表页面右上角单击**接入应用**。

4.  在**接入应用**页面顶部复制License Key。

    ![应用监控LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4864087161/p132858.png)


## 步骤二：安装ARMS应用监控组件

安装ARMS应用监控组件ack-arms-pilot。

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏选择**市场** \> **应用目录**，在右侧页面单击**ack-arms-pilot**。

3.  在应用目录 - ack-arms-pilot页面上，在右侧的创建面板中选择前提条件中创建的集群，并单击**创建**。


## 步骤三：安装Hercules Deploy组件上报PHP应用数据

1.  在本地新建一个YAML文件并命名为hercules.yaml，然后将以下内容拷贝至该YAML文件中。



    其中，您需要根据所在地域将YAML文件中的image的值替换为以下地址。

    |地域|下载地址|
    |--|----|
    |华东1（杭州）|    ```
registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华东2（上海）|    ```
registry.cn-shanghai.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北1（青岛）|    ```
registry.cn-qingdao.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北2（北京）|    ```
registry.cn-beijing.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北3（张家口）|    ```
registry.cn-zhangjiakou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华南1（深圳）|    ```
registry.cn-shenzhen.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |中国（香港）|    ```
registry.cn-hongkong.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |亚太东南（新加坡）|    ```
registry.ap-southeast-1.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |

2.  执行以下命令，安装Hercules Deploy组件。

    ```
    kubectl create -f hercules.yaml
    ```

    **说明：** 如果执行命令后提示Namespace已存在，请忽略。


## 步骤四：为PHP应用开启ARMS应用监控

1.  在[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)左侧导航栏选择**集群**，在**集群列表**页面上的目标集群右侧**操作**列单击**应用管理**。

2.  在无状态页面右上角单击**使用模板创建**。

3.  在使用模板创建页面上选择**示例模板**，并在**模板**（YAML格式）中将以下`annotations`添加到spec \> template \> metadata层级下。

    ```
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"
      armsAppType: PHP                                
    ```

    **说明：** 请将<your-deployment-name\>替换为您的应用名称。

4.  （本步骤仅限首次安装时）在和您的应用相同的命名空间下，创建arms-<yourAppName\>.ini的ConfigMap文件，并将以下内容复制至该文件中。

    ```
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: arms-<yourAppName>.ini
      namespace: <yourAppNamespace>
    data:
      arms.ini: |
        extension=/usr/local/arms/arms-php-agent/arms-[x.y].so
        [ARMS]
        arms.enable=1
        arms.app_name=<yourAppName>
        arms.license_key=<yourLicenseKey>
        arms.agent_env=PHPK8S
        arms.network_type=tcp
        arms.tcp_host=arms-hercules-service.arms-pilot
        arms.tcp_port=11234
    ```

    **说明：**

    -   请将<yourAppName\>替换为您的应用名称。
    -   请将<yourAppNamespace\>替换为您应用所在的命名空间。
    -   请将<yourLicenseKey\>替换为您在ARMS控制台的**接入应用**页面获取的LicenseKey。
    -   在`extension=/usr/local/arms/arms-php-agent/arms-[x.y].so`配置中，`arms-[x.y].so`的`[x.y]`为PHP应用的版本，支持的版本值为5.4、5.5、5.6、7.0、7.1、7.2和7.3。
    -   如果您的容器镜像是Alpine Linux系统，请将`arms-[x.y].so`改为`arms-[x.y]-alpine.so`，其中`[x.y]`支持的版本值为5.5、5.6、7.0、7.1、7.2和7.3。
    -   该ConfigMap文件与应用属于一一对应关系，如果需要接入其他应用，请重新创建一份单独的配置，并在不需要使用时删除该文件。
5.  将arms-<yourAppName\>.ini的ConfigMap配置项添加到应用Deployment的spec \> template \> spec \> containers配置下，将mountPath设置为PHP配置文件扫描目录路径。

    ```
    volumeMounts:
    - mountPath: /etc/php/7.2/fpm/conf.d/arms.ini
      name: arms-ini
      subPath: arms.ini
    ```

    其中`/etc/php/7.2/fpm/conf.d/`为PHP应用的配置加载目录地址，接着在spec \> template \> spec \> volumes下添加以下内容。

    ```
    volumes:
    - name: arms-ini
      configMap:
        name: arms-<yourAppName>.ini
    ```

    **说明：** 如果PHP没有配置文件扫描路径，请将arms-<yourAppName\>.ini配置项内容合并到应用的php.ini中。

    在[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)的无状态或有状态（StatefulSet）页面上，如果目标应用的**操作**列出现**ARMS控制台**按钮，则表示Agent安装成功。

    ![ARMS Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6606163161/p53712.png)

    **说明：** 若**操作**列没有出现**ARMS控制台**按钮，请检查您是否已授权容器服务访问ARMS资源。


## 卸载Agent

1.  如果需要临时暂停Agent，则将[步骤](#step_ha3_6ov_alh)添加的ConfigMap文件删除，然后再重新部署应用即可。

2.  如果需要卸载Agent，则删除[步骤](#step_y4n_031_gfg)添加的Hercules Deploy组件和[步骤](#step_ha3_6ov_alh)添加的ConfigMap文件。


## 常见问题

Agent安装失败怎么处理？

可能原因：arms-pilot的版本在v1.30以下。

解决方案：为容器服务Kubernetes版授予ARMS资源的访问权限。具体操作，请参见[Agent安装失败怎么处理？](/cn.zh-CN/应用监控/应用监控常见问题.md)。

## 更多信息

若您还有其他问题，可加入我们的钉钉答疑群：23328286。

