# Use SkyWalking to report Java application data

Before you can view the trace data of your application in the Tracing Analysis console, you must use a client to report the trace data to Tracing Analysis. This topic shows you how to use SkyWalking to report the data of Java applications.

-   SkyWalking 6.X.X, 7.X.X, or 8.X.X is downloaded from the [Download the SkyWalking releases](http://skywalking.apache.org/downloads/) page. We recommend that you download [SkyWalking 8.0.1](https://www.apache.org/dyn/closer.cgi/skywalking/8.0.1/apache-skywalking-apm-8.0.1.tar.gz). The decompressed folder Agent is placed in a directory that can be accessed by Java processes.
-   All plug-ins are placed in the `/plugins` directory. If you add a plug-in to the directory during the startup phase, the plug-in takes effect. If you delete a plug-in from the directory, the plug-in becomes ineffective. By default, log files are saved in the `/logs` directory.

**Warning:** Logs, plug-ins, and configuration files are all placed in the Agent folder. Do not change the folder structure.



SkyWalking is a popular application performance monitoring \(APM\) service developed in China. SkyWalking is designed for microservices, cloud-native architectures, and container-based architectures. Container-based architectures include Docker, Kubernetes, and Mesos. The core of SkyWalking is a distributed tracing system, which is a top-level project of Apache Software Foundation.

To use SkyWalking to report Java application data to the Tracing Analysis console, you must first instrument the application. SkyWalking not only provides auto-instrument agents such as Dubbo, gRPC, JDBC, OkHttp, Spring, Tomcat, Struts, and Jedis, but also allows you to manually instrument applications. This topic shows you how to automatically instrument applications.

## Use SkyWalking to automatically instrument a Java application

1.  Open the `config/agent.config` file and configure the endpoint and token.

    **Note:** Please`<endpoint>`And`<auth-token>`Replace them with the consoleOverviewThe endpoint and authentication token of the SkyWalking client in the corresponding region are displayed on the page. For more information, see [How to get Endpoint and Security Token](#tab3).

    ```
    collector.backend_service=<endpoint>
    agent.authentication=<auth-token>
    ```

2.  Use one of the following methods to set the service name of the application:

    **Note:** Replace `<ServiceName>` with your application name. If you use both of the following methods, only the second method that adds a parameter to the start command takes effect.

    -   Open the `config/agent.config` file and set the application name.

        ```
        agent.service_name=<ServiceName>
        ```

    -   Add the -Dskywalking.agent.service\_name parameter to the start command of the application.

        ```
        java -javaagent:<skywalking-agent-path> -Dskywalking.agent.service_name=<ServiceName> -jar yourApp.jar
        ```

3.  Use one of the following methods to specify the path to the Agent folder based on the runtime environment of the application:

    **Note:** Replace `<skywalking-agent-path>` in the following sample code with the absolute path of the skywalking-agent.jar file in the Agent folder.

    -   Linux Tomcat 7 / Tomcat 8

        Add the following content as the first line in the `tomcat/bin/catalina.sh` file:

        ```
        CATALINA_OPTS="$CATALINA_OPTS -javaagent:<skywalking-agent-path>"; export CATALINA_OPTS
        ```

    -   Windows Tomcat 7 / Tomcat 8

        Add the following content as the first line in the `tomcat/bin/catalina.bat` file:

        ```
        set "CATALINA_OPTS=-javaagent:<skywalking-agent-path>"
        ```

    -   JAR File or Spring Boot

        Add the -javaagent parameter to the start command of the application.

        **Note:** The -javaagent parameter must be written before the -jar parameter.

        ```
        java -javaagent:<skywalking-agent-path> -jar yourApp.jar
        ```

    -   Jetty

        Add the following content to the `{JETTY_HOME}/start.ini` configuration file:

        ```
        --exec    # Remove the number sign (#) to uncomment the code.
        -javaagent:<skywalking-agent-path>
        ```

4.  Restart the application.


## FAQ

Q: Why am I unable to create an application after SkyWalking is properly connected to the server?

A: The data may not be reported to Tracing Analysis. You must check whether the data is reported to Tracing Analysis. For example, you can check the content in the \{skywalking agent path\}/logs/skywalking-api.log file. If the result in the following figure is returned, the data is reported.

![pg_xtrace_skywalking](../images/p89094.png)

If no data is reported, check whether sampling is enabled, the data is filtered, or the request for using Tracing Analysis is not triggered.

[Apache SkyWalking official website](http://skywalking.apache.org/)

[Download the SkyWalking releases](http://skywalking.apache.org/downloads/)

[Deploy the Skywalking Java agent](https://github.com/apache/incubator-skywalking/blob/v5.0.0-GA/docs/cn/Deploy-skywalking-agent-CN.md)

