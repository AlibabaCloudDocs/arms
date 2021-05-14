# Versions of the ARMS agents

This topic describes the version history of the ARMS agents for Java and PHP.

## Versions of the ARMS agent for Java

|Version|Release date|Revision|
|-------|------------|--------|
|2.7.1.1|August 14, 2020|-   NoSQL monitoring is supported.
-   Routing of microservice tags is supported.
-   Compression for N + 1 invocations is supported.
-   The network connection issue of Finance Cloud is fixed and the memory usage is optimized. |
|2.7.1|July 16, 2020|-   The latest version of the Jedis plug-in is supported to fix the issue where topology maps are not recognized by ApsaraDB for Redis clusters. |
|2.7.0|May 20, 2020|-   Subfeatures of microservices are supported. |
|2.6.2|May 20, 2020|-   Business monitoring is supported. |
|2.6.1.2|March 19, 2020|-   Microservice authentication is supported.
-   Graceful disconnection for microservices is supported. |
|2.6.1.1|March 16, 2020|-   Components such as Spring Cloud Gateway and Spring Webflux are supported. |
|2.6.1|February 14, 2020|-   Features such as obtaining the metadata of microservices are supported. |
|2.6.0.2|January 2, 2020|-   A new version of exception analysis is provided.
-   Issues of the Thrift plug-in are fixed. |
|2.6.0|December 17, 2019|-   Asynchronous traces are supported.
-   The invocation parameters of Dubbo and HSFProvider are recorded.
-   Several existing plug-in issues are fixed. |
|2.5.9.5|November 28, 2019|-   The jfinal-undertow plug-in is supported.
-   Several bugs are fixed, such as the failure to obtain Dubbo thread profiling data. |
|2.5.9.3|November 25, 2019|-   Tracing Analysis is integrated with ARMS.
-   Several bugs are fixed and the agent performance is optimized. |
|2.5.9|September 6, 2019|-   The denial-of-service \(DoS\) vulnerability of Fastjson is fixed.
-   The logic that is used to obtain the IP addresses of network interface controllers is modified. |
|2.5.8|August 2, 2019|-   The dual-state alerting feature is supported. This allows you to configure alert rules for metrics that have only two states: yes and no or being and not being.
-   The plug-ins of Dameng Database, a database service provided by a Chinese company, are supported. |
|2.5.7.2|July 30, 2019|-   Metrics of Java Virtual Machine \(JVM\) Metaspace are supported.
-   HTTP status codes to be ignored can be customized. By default, all HTTP status codes greater than 400 are counted as errors. To ignore specific HTTP status codes greater than 400 so that they are not counted as errors, you can specify them in value. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options). |
|2.5.7|July 11, 2019|The dependent Fastjson version that has security vulnerabilities is upgraded. |
|2.5.6.1|June 28, 2019|-   Dubbo and MariaDB plug-ins are supported.
-   Bound SQL values can be obtained by custom configurations. The variable values bound to PrepareStatement can be captured. The variable values take effect without the need to restart the application. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options).
-   Memory is optimized and several bugs are fixed.
-   The dependency on Log4j is removed to prevent conflicts. |
|2.5.6|June 7, 2019|-   Quantile statistics are supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.5|June 3, 2019|-   HSF and HTTP calls are supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.3|March 15, 2019|-   Thread metrics can be reported when applications are running.
-   The Spring-Data-Redis plug-in is supported.
-   The plug-in of the Druid database connection pool is supported. |
|2.5.2|February 21, 2019|-   The number of file handles can be collected.
-   Instantaneous values for garbage collection \(GC\) time and for the number of GC operations can be reported.
-   The maximum length of request parameters can be customized. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options). |
|2.5.1|January 14, 2019|-   Trace compression is supported. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options).
-   Application monitoring jobs can be created without the need to use the ARMS console.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.5.0|December 28, 2018|-   The ARMS agent can be connected without the need to restart the application.
-   Host monitoring is improved and the Windows operating system is supported.
-   Spring Webflux is supported.
-   Features of the ARMS agent are optimized and several bugs are fixed. |
|2.4.6|October 26, 2018|-   The Google Remote Procedure Call \(gRPC\), Thrift, and XMemcached plug-ins are supported.
-   Topology views of API calls are supported.
-   Topology views that cover the frontend and backend are supported. |
|2.4.5|September 17, 2018|-   The Lettuce plug-in \(JRE 1.8+\) is supported.
-   The MongoDB plug-in is supported.
-   Exception details can be captured. |
|2.4.4|August 6, 2018|-   Thread profiling data of applications can be reported.
-   Memcached caching is supported.
-   Exception filtering can be customized. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options). |
|2.4.3.1|June 29, 2018|-   WebLogic servers are supported.
-   Undertow servers are supported.
-   Memory usage by the ARMS agent is optimized.
-   The time required to start and load the ARMS agent is shortened.
-   The issue where JVM monitoring and host monitoring metrics cannot be reported is fixed. |
|2.4.3|May 18, 2018|-   The monitoring metrics of Message Queue for Apache RocketMQ can be captured.
-   Monitoring methods can be customized.
-   The issue of frequent log output in throttling scenarios is fixed.
-   The maximum length of the method stack can be customized. For more information, see [\[Custom configuration\]](t152246.md#sc_advanced_options).
-   The sampling feature is optimized. Abnormal traces are excluded. |
|2.4.2|April 19, 2018|-   Custom configuration details can be read.
-   Trace information can be retrieved by using SDKs.
-   JVM metrics such as threads, the number of GC operations, and the duration of GC operations can be collected.
-   HSF calls can be monitored.
-   Host monitoring metrics related to CPU, memory, networks, and disks can be collected.
-   The issue where the ./shutdown.sh process may be stuck in the Tomcat environment is fixed. |
|2.4.1|March 24, 2018|-   JVM monitoring, such as the reporting of heap memory and non-heap memory is supported.
-   Play FrameWork 1.4.4 is supported.
-   Parameters such as the sampling rate, agent switch, log level, and threshold can be customized. For more information, see [\[Custom configuration\]](t152246.md#). |
|2.4.0|February 14, 2018|-   PostgreSQL databases are supported.
-   ARMS can be connected to Alibaba Cloud Elastic Compute Service \(ECS\) instances in each region over the internal network.
-   ARMS application monitoring is available for commercial use. |

## Versions of the ARMS agent for PHP

|Version|Release date|Revision|
|-------|------------|--------|
|3.0.1|December 16, 2020|-   The issue of failed requests caused by the PHP 5.x plug-in is fixed.
-   The Memcached, GuzzleHttp, and Message Queue for RabbitMQ plug-ins are supported. |
|3.0.0|June 19, 2020|A new version of the ARMS agent is provided and the agent performance is greatly optimized.|
|2.0.3|August 19, 2019|-   The Predis plug-in is supported.
-   Bugs of the Curl plug-in are fixed. |
|2.0.2|July 31, 2019|-   Issues in the transmission of network modules under high concurrency are fixed.
-   The logic for transmission and re-connection is redesigned.
-   The memory usage is reduced.
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
-   Bugs of host monitoring are fixed.
-   The php -m command can be run to show the ARMS version.
-   Domain Name System \(DNS\) is used to resolve the domain names of collectors.
-   Features of the ARMS agent are optimized and several bugs are fixed.

**Note:** We recommend that you immediately upgrade the ARMS agent from version 1.x.x to 2.x.x. |
|1.0.1|March 15, 2019|-   Laravel 5.x is supported.
-   The PDO plug-in is supported.
-   Unnecessary logs are removed.
-   Several bugs are fixed.

**Note:** We recommend that you immediately upgrade the ARMS agent from version 1.x.x to 2.x.x. |

