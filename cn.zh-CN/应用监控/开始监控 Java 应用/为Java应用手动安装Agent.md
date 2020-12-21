# 为Java应用手动安装Agent

为Java应用安装Agent后，ARMS即可开始监控Java应用，您可以查看应用拓扑、调用链路、异常事务、慢事务和SQL分析等一系列监控数据。您可以选择以手动方式或脚本方式安装Agent，本文介绍如何为Java应用手动安装Agent。

-   确保您使用的云服务器ECS实例的安全组已开放8442、8443、8883三个端口的TCP出方向权限。为云服务器ECS开放出方向权限的方法，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

    **说明：** ARMS不仅可接入阿里云ECS上的应用，还能接入其他能访问公网的服务器上的应用。

-   确保您使用的第三方组件或框架在应用监控兼容性列表范围内，请参见[应用监控兼容性列表](/cn.zh-CN/应用监控/参考信息/ARMS应用监控支持的Java组件和框架.md)。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。


## 操作步骤

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

3.  在应用列表页面右上角单击**接入应用**。

4.  在接入应用页面执行以下操作：

    1.  在**请先选择您使用的语言**区域选择**Java**。

    2.  在**请先选择您使用的环境**区域选择**默认**。

    3.  在**请选择以下接入方式**区域选择**手动安装**。

5.  采用以下任一方法下载Agent，然后在控制台接入应用页面的下载Agent页签中单击**下一步**。

    -   方法一：手动下载。在下载Agent页签中单击**下载Agent**。
    -   方法二：使用Wget命令下载。根据您的地域下载对应的Agent安装包。

        **说明：** 请使用公网地址，如无法下载则使用VPC地址。

        |地域|公网地址|VPC地址|
        |--|----|-----|
        |华东1（杭州）|        ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华东2（上海）|        ```
wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华北1（青岛）|        ```
wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华北2（北京）|        ```
wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华北3（张家口）|        ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华南1（深圳）|        ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |中国（香港）|        ```
wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |亚太东南（新加坡）|        ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |日本（东京）|        ```
wget "http://arms-apm-japan.oss-ap-northeast-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-japan.oss-ap-northeast-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |美西（硅谷）|        ```
wget "http://arms-apm-usw.oss-us-west-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-usw.oss-us-west-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华东1金融云|        ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华东2金融云|        ```
wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |
        |华南1金融云|        ```
wget "http://arms-apm-sz-finance.oss-cn-shenzhen-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ```

|        ```
wget "https://arms-apm-sz-finance.oss-cn-shenzhen-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        ``` |

6.  进入Agent安装包所在目录，并执行以下命令来解压安装包到任意工作目录下。

    ```
    unzip ArmsAgent.zip -d /{user.workspace}/ 
    ```

    **说明：** \{user.workspace\}是示例目录，请替换为真实的目录。

7.  在**接入应用**页面顶部复制License Key。

    ![应用监控LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6570348951/p132858.png)

8.  采用以下任一方法来添加AppName和LicenseKey参数。

    **说明：** 请将示例代码中的`{LicenseKey}`替换成您的License Key，将`{AppName}`替换成您的应用名称（应用名不可包含中文字符），将`{user.workspace}`替换成实际Agent安装包的解压目录，将demoApp.jar替换为真实的JAR包地址。

    -   方法一：根据您的应用运行环境修改JVM参数。

        |运行环境|步骤|
        |----|--|
        |Tomcat（Linux或macOS操作系统）|在\{TOMCAT\_HOME\}/bin/setenv.sh文件中添加以下配置。

        ```
JAVA_OPTS="$JAVA_OPTS -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}" 
        ```

如果您的Tomcat版本没有setenv.sh配置文件，请打开\{TOMCAT\_HOME\}/bin/catalina.sh文件，并在JAVA\_OPTS后添加上述配置，具体示例，请参见[catalina.sh](https://arms-public.oss-cn-shanghai.aliyuncs.com/arms-agent/catalina.sh)的第256行。 |
        |Tomcat（Windows操作系统）|在\{TOMCAT\_HOME\}/bin/catalina.bat文件中添加以下配置：        ```
set "JAVA_OPTS=%JAVA_OPTS% -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}" 
        ```

如果以上配置未生效，可以尝试在\{TOMCAT\_HOME\}/bin/catalina.bat文件中添加以下配置：

        ```
set "CATALINA_OPTS=-javaagent:/{user.workspace}/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}"
        ``` |
        |Jetty|在\{JETTY\_HOME\}/start.ini配置文件中添加以下配置：

        ```
--exec
-javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
-Darms.licenseKey={LicenseKey}
-Darms.appName={AppName} 
        ``` |
        |Spring Boot|启动Spring Boot进程时，在启动命令后加上-javaagent参数：

        ```
java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -jar demoApp.jar 
        ``` |
        |Resin|启动Resin进程时，在conf/resin.xml配置文件中添加以下标签：

        ```
<server-default>
    <jvm-arg>-javaagent:{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar</jvm-arg>
    <jvm-arg>-Darms.licenseKey={LicenseKey}</jvm-arg>
    <jvm-arg>-Darms.appName={AppName}</jvm-arg>
</server-default> 
        ```

在conf/app-default.xml文件中添加以下标签：

        ```
<library-loader path="{user.workspace}/ArmsAgent/plugin"/> 
        ``` |
        |Windows|启动Java进程时，在挂载Agent路径中使用反斜线（\\）作为分隔符。

        ```
{CMD}} java -javaagent:\{user.workspace}\ArmsAgent\arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -jar {user.workspace}\demoApp.jar 
        ``` |

        如需在一台服务器上部署同一应用的多个实例，可以通过-Darms.agentId参数（逻辑编号）来区分接入的JVM进程，例如：

        ```
        java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -Darms.agentId=001 -jar demoApp.jar
        ```

    -   方法二：
        1.  在arms-agent.config文件中添加以下配置。

            ```
            arms.licenseKey={LicenseKey} arms.appName={AppName}
            ```

        2.  在Java应用的启动脚本中添加以下参数。

            ```
            -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar 
            ```

9.  重启Java应用。


## 结果验证

约一分钟后，若Java应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载Agent

当您不需要使用ARMS监控您的Java应用时，请按照以下步骤卸载Agent：

1.  删除[步骤](#step_configure_licensekey)添加的\{AppName\}、\{LicenseKey\}等所有参数。

2.  重启Java应用。


## 快速更改应用名称

如需更改应用名称，例如忘记将示例应用名称Java-Demo修改为自定义名称，您可以在不重启应用、不重装Agent的情况下更改应用名称，具体操作，请参见[以通用方式安装Agent的普通Java应用如何更改应用名称？](/cn.zh-CN/应用监控/应用监控常见问题.mdsection_sx9_df1_3pq)。

## 更多信息

**相关文档**  


[应用监控常见问题](/cn.zh-CN/应用监控/应用监控常见问题.md)

