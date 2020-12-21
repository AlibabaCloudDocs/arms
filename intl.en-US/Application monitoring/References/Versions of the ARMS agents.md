# Versions of the ARMS agents

This topic describes the version history of the ARMS agents for Java and PHP.

## Versions of the ARMS agent for Java

|Version|Release date|Revision|
|-------|------------|--------|
|2.7.1.1|August 14, 2020|-   NoSQL monitoring is supported.
-   Routing of microservice tags is supported.
-   Compression for N + 1 invocations is supported.
-   The network connection issue of Finance Cloud is fixed and the memory usage is optimized. |
|2.7.1|July 16, 2020|-   The latest version of the Jedis plug-in is supported to solve the issue that topology maps are not recognized by ApsaraDB for Redis clusters. |
|2.7.0|May 20, 2020|-   Subfeatures of microservices are supported. |
|2.6.2|May 20, 2020|-   Business monitoring is supported. |
|2.6.1.2|March 19, 2020|-   Microservice authentication is supported.
-   Graceful disconnection for microservices is supported. |
|2.6.1.1|March 16, 2020|-   Components such as Spring Cloud Gateway and Spring Webflux are supported. |
|2.6.1|February 14, 2020|-   Features such as obtaining microservice metadata are supported. |
|2.6.0.2|January 2, 2020|-   Exception analysis of the new version is supported.
-   The Thrift plug-in issue is fixed. |
|2.6.0|December 17, 2019|-   Asynchronous trace is supported.
-   The invocation parameters of Dubbo and HSFProvider are recorded.
-   Several existing plug-in issues are fixed. |
|2.5.9.5|November 28, 2019|-   The jfinal-undertow plug-in is supported.
-   Several bugs are fixed, such as the failure to obtain Dubbo thread profiling data. |
|2.5.9.3|November 25, 2019|-   Tracing services are integrated into ARMS.
-   Several bugs are fixed and the agent performance is optimized. |
|2.5.9|September 6, 2019|-   The denial of service \(DoS\) vulnerability of FastJson is fixed.
-   The logic that is used to obtain the IP address of network interface controller is modified. |
|2.5.8|August 2, 2019|-   The dual-state alert feature is supported. This feature is used to configure alert rules for metrics with the only two states: yes or no.
-   Chinese DM database plug-ins are supported. |
|2.5.7.2|July 30, 2019|-   JVM metaspace metrics are supported.
-   HTTP status codes to be ignored can be customized. By default, status codes greater than 400 are counted as errors. You can also customize a threshold greater than 400. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options). |
|2.5.7|July 11, 2019|The FastJson version of dependencies is upgraded to eliminate security vulnerabilities. |
|2.5.6.1|June 28, 2019|-   Dubbo and MariaDB plug-ins are supported.
-   Bound SQL values can be obtained by custom configurations. The variable values bound to PrepareStatement can be captured. The variable values take effect without the need to restart the application. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options).
-   Memory is optimized and several bugs are fixed.
-   Log4j log dependency is removed to avoid conflicts. |
|2.5.6|June 7, 2019|-   Quantile statistics is supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.5|June 3, 2019|-   HSF and HTTP calls are supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.3|March 15, 2019|-   Thread metrics of application can be reported while the applications are running.
-   The Spring-Data-Redis plug-in is supported.
-   The Druid database connection pool plug-in is supported. |
|2.5.2|February 21, 2019|-   The number of file handles can be collected.
-   Instantaneous values for garbage collection \(GC\) time and for the number of GC operations can be reported.
-   The maximum length of request parameters can be customized. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options). |
|2.5.1|January 14, 2019|-   Trace compression is supported. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options).
-   Application monitoring jobs can be created without the need to use the ARMS console.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.0|December 28, 2018|-   Agent can be connected without the need to restart the application.
-   Host monitoring is improved and the Windows system can be monitored.
-   Spring-webflux is supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.4.6|October 26, 2018|-   The Google Remote Procedure Call \(gRPC\), Thrift, and XMemcached plug-ins are supported.
-   Topology views of API operation calls are supported.
-   Topology views that cover the frontend and backend are supported. |
|2.4.5|September 17, 2018|-   The Lettuce plug-in \(JRE 1.8+ \) is supported.
-   The MongoDB plug-in is supported.
-   Exception details can be captured. |
|2.4.4|August 6, 2018|-   Application thread profiling data can be reported.
-   Memcached caching is supported.
-   Exception filtering can be customized. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options). |
|2.4.3.1|June 29, 2018|-   WebLogic servers are supported.
-   Undertow servers are supported.
-   Memory usage by the ARMS agent is optimized.
-   The time required to start and load the ARMS agent is shortened.
-   The problem that JVM monitoring and host monitoring metrics cannot be reported is eliminated. |
|2.4.3|May 18, 2018|-   The monitoring metrics of Message Queue for RocketMQ \(RocketMQ\) can be captured.
-   Monitoring methods can be customized.
-   The problem of frequent log output in throttling scenarios is solved.
-   The maximum length of the method stack can be customized. For more information, see [\[ Related topic\]](t152246.md#sc_advanced_options).
-   The sampling feature is optimized. Abnormal traces are excluded. |
|2.4.2|April 19, 2018|-   Custom configuration details can be read.
-   Trace information can be retrieved by using SDKs.
-   JVM metrics such as thread, number of GC operations, and duration of GC operations can be collected.
-   HSF calls can be monitored.
-   Host monitoring metrics related to CPU, memory, networks, and disks can be collected.
-   The problem that the ./shutdown.sh process may be stuck in the Tomcat environment is eliminated. |
|2.4.1|March 24, 2018|-   JVM monitoring, such as reporting of heap memory and non-heap memory is supported.
-   PlayFrameWork 1.4.4 is supported.
-   Parameters such as the sampling rate, agent switch, log level, and threshold can be customized. For more information, see [\[ Related topic\]](t152246.md#). |
|2.4.0|February 14, 2018|-   The PostgreSQL database is supported.
-   ARMS can be connected with Alibaba Cloud Elastic Compute Service \(ECS\) instances in each region over the internal network.
-   ARMS application monitoring is available for commercial use. |

## Versions of the ARMS agent for PHP

|Version|Release date|Revision|
|-------|------------|--------|
|2.0.3|August 19, 2019|-   The Predis plug-in is supported.
-   Bugs of the Curl plug-in are fixed. |
|2.0.2|July 31, 2019|-   Issues in the transmission of network modules under high concurrency are fixed.
-   The logic for transmission and re-connection is redesigned.
-   Memory usage is reduced.
-   Several bugs are fixed. |
|2.0.1|July 23, 2019|-   The Arms-agent process is used as the daemon.
-   The Redis and MongoDB plug-ins are supported.
-   Several bugs are fixed. |
|2.0.0|July 5, 2019|-   A new and more reliable network model is used.
-   The display of exception information is optimized.
-   The memory usage is optimized.
-   Several bugs are fixed. |
|1.1.0|April 30, 2019|-   The GCC 4.4.7 environment is supported.
-   The TCP connection heartbeat is introduced.
-   Host monitoring bugs are fixed.
-   php -m command can be run to show the ARMS version.
-   DNS is used to resolve the domain names of collectors.
-   Features of the ARMS agent are optimized and several bugs are fixed.

**Note:** We recommend that you immediately upgrade the ARMS agent from version 1.x.x to 2.x.x. |
|1.0.1|March 15, 2019|-   Laravel 5.x is supported.
-   The PDO plug-in is supported.
-   Unnecessary logs are removed.
-   Several bugs are fixed.

**Note:** We recommend that you immediately upgrade the ARMS agent from version 1.x.x to 2.x.x. |

