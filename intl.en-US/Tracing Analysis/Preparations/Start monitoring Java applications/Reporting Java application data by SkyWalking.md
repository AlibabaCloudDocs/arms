# Reporting Java application data by SkyWalking

Before using the tracing analysis console to trace tracing data, you need to report the data to the tracing analysis console from the client. This topic describes how to use the Skywalking client to report Java application data.

-   Open [skywalking download page](http://skywalking.apache.org/downloads/) download SkyWalking 6.X.X, 7.X. X or 8.X. X \(it is recommended to download [skywalking 8.0.1](https://www.apache.org/dyn/closer.cgi/skywalking/8.0.1/apache-skywalking-apm-8.0.1.tar.gz)\) and the decompressed Agent folder put to the Java process that has access to the Directory
-   Plug-ins are placed in the `/plugins` directory. Place the new plug-in in the directory during the startup phase to make the plug-in take effect. Delete the plug-in from the directory to disable the plug-in. In addition, the log files are automatically output to the `/logs` directory.

**Warning:** Logs, plug-ins, and configuration files are all in the Agent folder. Do not change the folder structure.



SkyWalking is a popular Application Performance Monitoring \(APM\) product made in China. It is mainly aimed at microservices, Cloud-Native, and containerized applications such as Docker, Kubernetes, and Mesos. SkyWalking is a distributed tracing system at its core, and is currently a top-level project of the Apache Foundation.

To report Java application data to the link tracking console by using SkyWalking, you must first complete tracking. SkyWalking supports both automatic probe \(Dubbo, gRPC, JDBC, OkHttp, Spring, Tomcat, Struts, and Jedis\) and manual tracing \(OpenTracing\). This article introduces the automatic tracking method.

## Automatic Tracking for Java applications with SkyWalking

1.  Open `config/agent.config` and configure the access point and token.

    **Note:** Please`<endpoint>`And`<auth-token>`Replace them with the consoleOverviewThe endpoint and authentication token of the SkyWalking client in the corresponding region are displayed on the page. For more information, see [How to get Endpoint and Security Token](#tab3).

    ```
    
            collector.backend_service=<endpoint> agent.authentication=<auth-token> 
          
    ```

2.  Use either of the following methods to set the Service Name.

    **Note:** Replace `<ServiceName> with` your application name. If you use both of the following methods, only the second method \(added to the startup command line\) takes effect.

    -   Open `config/agent.config` and configure the application name.

        ```
        
                 agent.service_name=<ServiceName> 
               
        ```

    -   Add the -Dskywalking.agent.service\_name parameter to the application's startup command line.

        ```
        
                 java -javaagent:<skywalking-agent-path> -Dskywalking.agent.service_name=<ServiceName> -jar yourApp.jar 
               
        ```

3.  Use a method to specify the path of the SkyWalking Agent depending on the runtime environment of the application.

    **Note:** Replace the `following sample code <skywalking-agent-path> with`the absolute path of the skywalking-agent.jar in the Agent folder.

    -   Linux Tomcat 7 / Tomcat 8

        Add the following content to the first line of `tomcat/bin/catalina.sh`:

        ```
        
                 CATALINA_OPTS="$CATALINA_OPTS -javaagent:<skywalking-agent-path>"; export CATALINA_OPTS 
               
        ```

    -   Windows Tomcat 7 / Tomcat 8

        Add the following content to the first line of `tomcat/bin/catalina.bat`:

        ```
        
                 set "CATALINA_OPTS=-javaagent:<skywalking-agent-path>" 
               
        ```

    -   JAR File or Spring Boot

        Add the -javaagent parameter in the application's startup command line.

        **Note:** -Javaagent must be before -jar.

        ```
        
                 java -javaagent:<skywalking-agent-path> -jar yourApp.jar 
               
        ```

    -   Jetty

        Add the following content to the `https://jetty_home#/start.ini` configuration file:

        ```
        
                 -- exec# Remove the Front number to cancel the comment. -javaagent: <skywalking-agent-path> 
               
        ```

4.  Restart the application.


## FAQ

Q: Why cannot I create an application after I connect to the server through SkyWalking?

A: It may be because the tracing data has not been reported. You must check whether tracing data has been reported. For more information, see configure skywalking agent pathname/logs/skywalking-api.log. If data is reported, the output is as follows:

![pg_xtrace_skywalking](../images/p89094.png)

If no data is reported, the possible cause is that sampling is enabled, filtering is configured, or the link tracing request is not generated.

[SkyWalking official website](http://skywalking.apache.org/)

[Download SkyWalking](http://skywalking.apache.org/downloads/)

[Deployment SkyWalking Java Agent](https://github.com/apache/incubator-skywalking/blob/v5.0.0-GA/docs/cn/Deploy-skywalking-agent-CN.md)

