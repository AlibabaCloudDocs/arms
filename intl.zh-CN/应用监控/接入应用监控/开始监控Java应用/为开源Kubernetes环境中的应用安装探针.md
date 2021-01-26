# 为开源Kubernetes环境中的应用安装探针

借助ARMS应用监控，您可以对开源Kubernetes环境的应用进行应用拓扑、接口调用、异常事务和慢事务监控、SQL分析等监控。本文将帮助您将开源Kubernetes环境中的应用接入ARMS应用监控。

-   [开通ARMS服务](/intl.zh-CN/快速入门/开通和升级ARMS.md)。
-   [安装Helm](https://helm.sh/docs/intro/install/)。
-   确保您的Kubernetes api-server组件接口版本在1.10及以上。
-   确保您的集群连通公网。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。




## 步骤一：安装探针

ARMS应用监控目前仅支持无状态（Deployment）和有状态（StatefulSet）两种类型的应用接入，两种类型的应用接入方法相同。此处以将开源Kubernetes环境中的无状态（Deployment）类型的应用接入ARMS应用监控为例。

1.  采用以下方法之一下载arms-pilot。

    -   方法一：手动下载[最新安装包](http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz)。
    -   方法二： 执行以下`Wget`命令下载arms-pilot安装包。

        ```
        wget 'http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-pilot/arms-pilot-0.1.1-community.tgz' -O arms-pilot-0.1.1.tgz                                
        ```

2.  执行以下命令解压arms-pilot安装包。

    ```
    tar zxvf arms-pilot-0.1.1.tgz                         
    ```

3.  编辑安装包下的values.yaml文件，根据实际情况修改`uid`和`region_id`，然后保存。

    ```
    userId: __USER_ID__
    regionId: __REGION_ID__
    ```

4.  执行以下命令安装arms-pilot。

    ```
    helm install ./arms-pilot --namespace arms-pilot-system                        
    ```


## 步骤二：获取Licensekey

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏中选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

3.  在应用列表页面右上角单击**接入应用**。

4.  在接入应用页面顶部单击License Key右侧的复制图标，保存License Key。

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9141208061/p45312.png)


## 步骤三：修改应用的YAML文件

1.  执行以下命令查看目标无状态（Deployment）应用的YAML文件。

    ```
    kubectl get deployment {deployment名称} -o yaml                            
    ```

    **说明：** 若您不清楚`{deployment名称}`，请先执行以下命令查看所有无状态（Deployment）应用，在执行结果中找到目标无状态（Deployment）应用，再查看目标无状态（Deployment）应用的YAML文件。

    ```
    kubectl get deployments --all-namespace                
    ```

2.  启动编辑目标无状态（Deployment）应用的YAML文件。

    ```
    kubectl edit deployment {Deployment名称} -o yaml                        
    ```

3.  在YAML文件中的spec -\> template -\> metadata -\> labels层级下加入以下内容。

    ```
    ARMSApmAppName: xxx
    ARMSApmLicenseKey: xxx                           
    ```

    **说明：**

    -   请将`xxx`分别替换成您的LicenseKey和应用名称，应用名暂不支持中文。
    -   将LicenseKey中的符号`@`替换为符号`_`。
    如果您需要在开源K8s环境中创建一个新的无状态（Deployment）应用并接入ARMS，则应用的完整YAML文件如下：

4.  保存配置后，应用将自动重启，以上配置生效。

    2 ~ 5分钟后，若您的应用出现在ARMS控制台的**应用监控** \> **应用列表**中且有数据上报，则说明接入成功。


## 卸载探针

1.  当您不需要再监控开源Kubernetes环境中的Java应用时，可执行以下命令卸载arms-pilot。

    ```
    helm del --purge arms-pilot
    ```

2.  重启您的业务Pod。


**相关文档**  


[应用监控常见问题](/intl.zh-CN/应用监控/应用监控常见问题.md)

