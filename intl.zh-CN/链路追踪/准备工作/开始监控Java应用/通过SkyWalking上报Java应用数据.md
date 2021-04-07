# 通过SkyWalking上报Java应用数据

在使用链路追踪控制台追踪应用的链路数据之前，需要通过客户端将应用数据上报至链路追踪。本文介绍如何通过Skywalking客户端上报Java应用数据。

-   打开[SkyWalking下载页面](http://skywalking.apache.org/downloads/)，下载SkyWalking 6.X.X、7.X.X或8.X.X版本（建议下载[SkyWalking 8.0.1](https://www.apache.org/dyn/closer.cgi/skywalking/8.0.1/apache-skywalking-apm-8.0.1.tar.gz)），并将解压后的Agent文件夹放至Java进程有访问权限的目录。
-   插件均放置在`/plugins`目录中。在启动阶段将新的插件放进该目录，即可令插件生效。将插件从该目录删除，即可令其失效。另外，日志文件默认输出到`/logs`目录中。

**警告：** 日志、插件和配置文件都在Agent文件夹中，请不要改变文件夹结构。



SkyWalking是一款广受欢迎的国产APM（Application Performance Monitoring，应用性能监控）产品，主要针对微服务、Cloud Native和容器化（Docker、Kubernetes、Mesos）架构的应用。SkyWalking的核心是一个分布式追踪系统，目前是Apache基金会的顶级项目。

要通过SkyWalking将Java应用数据上报至链路追踪控制台，首先需要完成埋点工作。SkyWalking既支持自动探针（Dubbo、gRPC、JDBC、OkHttp、Spring、Tomcat、Struts、Jedis等），也支持手动埋点（OpenTracing）。本文介绍自动埋点方法。



## 用SkyWalking为Java应用自动埋点

1.  打开`config/agent.config`，配置接入点和令牌。

    **说明：** 请将`<endpoint>`和`<auth-token>`分别替换成控制台概览页面上SkyWalking客户端在相应地域的接入点和鉴权令牌。关于获取方法，请参见前提条件中的[获取SkyWalking接入点和鉴权令牌](#tab3)。

    ```
    collector.backend_service=<endpoint>
    agent.authentication=<auth-token>
    ```

2.  采用以下方法之一配置应用名称（Service Name）。

    **说明：** 请将`<ServiceName>`替换为您的应用名称。如果同时采用以下两种方法，则仅第二种方法（在启动命令行中添加参数）生效。

    -   打开`config/agent.config`，配置应用名称。

        ```
        agent.service_name=<ServiceName>
        ```

    -   在应用程序的启动命令行中添加-Dskywalking.agent.service\_name参数。

        ```
        java -javaagent:<skywalking-agent-path> -Dskywalking.agent.service_name=<ServiceName> -jar yourApp.jar
        ```

3.  根据应用的运行环境，选择相应的方法来指定SkyWalking Agent的路径。

    **说明：** 请将以下示例代码中的`<skywalking-agent-path>`替换为Agent文件夹中的skywalking-agent.jar的绝对路径。

    -   Linux Tomcat 7 / Tomcat 8

        在`tomcat/bin/catalina.sh`第一行添加以下内容：

        ```
        CATALINA_OPTS="$CATALINA_OPTS -javaagent:<skywalking-agent-path>"; export CATALINA_OPTS
        ```

    -   Windows Tomcat 7 / Tomcat 8

        在`tomcat/bin/catalina.bat`第一行添加以下内容：

        ```
        set "CATALINA_OPTS=-javaagent:<skywalking-agent-path>"
        ```

    -   JAR File或Spring Boot

        在应用程序的启动命令行中添加-javaagent参数。

        **说明：** -javaagent参数一定要在-jar参数之前。

        ```
        java -javaagent:<skywalking-agent-path> -jar yourApp.jar
        ```

    -   Jetty

        在`{JETTY_HOME}/start.ini`配置文件中添加以下内容：

        ```
        --exec    # 去掉前面的井号取消注释。
        -javaagent:<skywalking-agent-path>
        ```

4.  重新启动应用。


## 常见问题

问：SkyWalking正常连接服务端后，无法创建应用？

答：可能是由于链路追踪的数据未上报。您需要检查是否有链路追踪的数据上报，可以查看\{skywalking agent path\}/logs/skywalking-api.log内容。如果有数据上报，则显示如下图所示。

![pg_xtrace_skywalking](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1804948951/p89094.png)

如果未产生数据上报，则可能原因是：开启采样、设置过滤或未触发生成链路追踪的请求。

[SkyWalking官网](http://skywalking.apache.org/)

[下载SkyWalking](http://skywalking.apache.org/downloads/)

[部署SkyWalking Java Agent](https://github.com/apache/incubator-skywalking/blob/v5.0.0-GA/docs/cn/Deploy-skywalking-agent-CN.md)

