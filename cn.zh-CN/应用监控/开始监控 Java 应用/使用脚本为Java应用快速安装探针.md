# 使用脚本为Java应用快速安装探针

ARMS提供一键接入方式为Java应用安装探针，安装成功后无需重启应用即可开始监控，适用于新手用户。当应用重启时，探针会自动加载，该Java应用将自动接入ARMS应用监控。

-   确保您使用的云服务器ECS实例的安全组已开放8442、8443、8883三个端口的TCP出方向权限。为云服务器ECS开放出方向权限的方法，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

    **说明：** ARMS不仅可接入阿里云ECS上的应用，还能接入其他能访问公网的服务器上的应用。

-   确保您使用的第三方组件或框架在应用监控兼容性列表范围内，请参见[应用监控兼容性列表](/cn.zh-CN/应用监控/参考信息/ARMS应用监控支持的Java组件和框架.md)。
-   若您的应用已经按照手动接入方式接入ARMS应用监控，则需先卸载探针才能正常使用一键接入方式，请参见[卸载探针](/cn.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。


## 操作步骤

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏中选择**应用监控** \> **应用列表**。

3.  在应用列表页面顶部选择目标地域，在右上角单击**接入应用**。

4.  在接入应用页面执行以下操作：

    1.  在请先选择您使用的语言区域选择**Java**。

    2.  在请先选择您使用的环境区域选择**默认**。

    3.  在请选择以下接入方式区域选择**脚本安装**。

    ![Access Agent](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9184928061/p44367.png)

5.  在接入应用页面顶部复制License Key。

6.  运行您所在地域对应的安装脚本。

    |地域|安装脚本|
    |--|----|
    |华东1（杭州）|    ```
wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |华东2（上海）|    ```
wget -O- http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |华北1（青岛）|    ```
wget -O- http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |华北2（北京）|    ```
wget -O- http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |华南1（深圳）|    ```
wget -O- http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |中国（香港）|    ```
wget -O- http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |亚太东南（新加坡）|    ```
wget -O- http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |日本（东京）|    ```
wget -O- http://arms-apm-japan.oss-ap-northeast-1.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |美国（硅谷）|    ```
wget -O- http://arms-apm-usw.oss-us-west-1.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |华东1金融云|    ```
wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |

    **说明：**

    -   将`<licenseKey>`替换为您的LicenseKey。
    -   将`Java-Demo`替换成您的应用名，应用名暂不支持中文。
    -   执行安装脚本后，该脚本会自动下载最新探针。
    -   若您的服务器只有一个Java进程，安装脚本会默认选择该进程安装探针；若您的服务器有多个Java进程，请根据提示选择一个进程安装探针。

## 结果验证

约一分钟后，若您的应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载探针

1.  当您不需要使用ARMS监控您的Java应用时，执行`jps -l`命令查看所有进程，并在执行结果中找到`com.alibaba.mw.arms.apm.supervisor.daemon.Daemon`对应的进程号。

    在本示例中，`com.alibaba.mw.arms.apm.supervisor.daemon.Daemon`对应的进程号为：62857。

    ![Kill Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2970348951/p43111.png)

2.  执行命令`kill -9 <进程号>`。

    例如：`kill -9 62857`。

3.  执行`rm -rf /.arms /root/.arms`。

4.  重启您的应用。


## 快速更改应用名称

如果因为某些原因希望更改应用名称，例如忘记将示例应用名称Java-Demo修改为自定义名称，您可以在不重启应用、不重装探针的情况下更改应用名称，详情参见[以快速方式安装探针的普通Java应用如何更改应用名称](/cn.zh-CN/应用监控/应用监控常见问题.mdsection_dv7_df9_oz2)。

## 常见问题

1.  如果在执行一键接入Java应用脚本时出现以下getcwd相关错误该怎么处理？

    ```
    shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory Error occurred during initialization of VM java.lang.Error: Properties init: Could not determine current working directory. at java.lang.System.initProperties(Native Method) at java.lang.System.initializeSystemClass(System.java:1119)
    ```

    可能原因是执行脚本过程中误删了当前目录。解决办法为：先执行`cd`，然后重新运行脚本。

2.  使用一键接入方式安装探针后，在哪里查看日志？

    日志的默认目录为：/root/.arms/supervisor/logs/arms-supervisor.log，若此目录下没有日志，请执行命令`ps -ef |grep arms`查看日志所在目录。


## 更多信息

**相关文档**  


[应用监控常见问题](/cn.zh-CN/应用监控/应用监控常见问题.md)

