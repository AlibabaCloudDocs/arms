# 为容器服务Kubernetes版Java应用安装探针

只需安装ARMS应用监控组件（探针），即可对部署在容器服务Kubernetes版中的Java应用进行监控，查看应用拓扑、接口调用、异常事务和慢事务等方面的监控数据。本文介绍如何为容器服务Kubernetes版Java应用安装探针。

-   [创建Kubernetes专有版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes专有版集群.md)
-   [管理命名空间](/cn.zh-CN/Kubernetes集群用户指南/命名空间与配额/管理命名空间.md)：本文示例中的命名空间名称为arms-demo。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。


## 步骤一：安装ARMS应用监控组件

安装ARMS应用监控组件ack-arms-pilot。

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏选择**市场** \> **应用目录**，在右侧页面单击**ack-arms-pilot**。

3.  在应用目录 - ack-arms-pilot页面上，在右侧的创建面板中选择前提条件中创建的集群，并单击**创建**。


## 步骤二：为Java应用开启ARMS应用监控

如需在创建新应用的同时开启ARMS应用监控，请按以下步骤操作：

1.  在[容器服务Kubernetes版控制台](https://cs.console.aliyun.com/#/k8s/overview)左侧导航栏选择**集群**，在**集群列表**页面上的目标集群右侧**操作**列单击**应用管理**。

2.  在无状态页面右上角单击**使用YAML创建资源**。

3.  在使用YAML创建资源页面上选择**示例模板**，并在**模板**（YAML格式）中将以下`annotations`添加到spec \> template \> metadata层级下。

    **说明：** 请将<your-deployment-name\>替换为您的应用名称。

    ```
    annotations:
      armsPilotAutoEnable: "on"
      armsPilotCreateAppName: "<your-deployment-name>"                                
    ```

    ![YAML Example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0446760061/p53707.png)

    创建一个无状态（Deployment）应用并开启ARMS应用监控的完整YAML示例模板如下：


## 执行结果

在无状态页面上，目标应用的**操作**列将出现**ARMS控制台**按钮。

![ARMS Console Button](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6606163161/p53712.png)

## 卸载探针

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏单击**集群**，在**集群列表**页面上的目标集群右侧**操作**列单击**应用管理**。

3.  在左侧导航栏选择**应用** \> **Helm**

4.  在Helm页面，ARMS Agent对应的发布名称**arms-pilot**右侧**操作**列，单击**删除**。

5.  在删除应用对话框单击**确定**。

6.  重启您的业务Pod。


## 常见问题

-   如何更改应用名称？

    如需更改应用名称，您需要修改Deployment内的armsPilotCreateAppName参数。具体操作，请参见[部署在容器服务K8s集群中的Java应用如何更改应用名称](/cn.zh-CN/应用监控/应用监控常见问题.md)。

-   Agent安装失败怎么处理？

    可能原因：arms-pilot的版本在v1.30以下。

    解决方案：为容器服务Kubernetes版授予ARMS资源的访问权限。具体操作，请参见[容器服务K8s集群中的Java应用安装Agent失败怎么处理？](/cn.zh-CN/应用监控/应用监控常见问题.md)。


## 更多信息

**相关文档**  


[创建Kubernetes专有版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes专有版集群.md)

[管理命名空间](/cn.zh-CN/Kubernetes集群用户指南/命名空间与配额/管理命名空间.md)

[为容器服务Kubernetes版PHP应用安装Agent](/cn.zh-CN/应用监控/接入应用监控/开始监控PHP应用/为容器服务Kubernetes版PHP应用安装Agent.md)

