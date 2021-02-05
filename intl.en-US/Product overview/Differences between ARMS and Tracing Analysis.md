# Differences between ARMS and Tracing Analysis

Both Application Real-Time Monitoring Service \(ARMS\) and Tracing Analysis can solve tracing problems in a distributed environment. This topic describes the differences between ARMS and Tracing Analysis.

## Background information

ARMS is an application performance management \(APM\) service provided by Alibaba Cloud. ARMS allows you to build application monitoring capabilities that feature response time within several seconds for enterprises from custom dimensions such as the browser, application, and business.

Tracing Analysis provides developers with various features for distributed application development, including trace mapping, request counting, trace discovery, and application dependency analytics. Tracing Analysis helps you analyze and diagnose performance bottlenecks in a distributed application architecture. It also makes microservice development and diagnostics efficient, and reduces the costs of developing tracing applications such as Jaeger and Zipkin and related storage services such as HBase and Elasticsearch.

## Comparison between ARMS and Tracing Analysis

|Difference|ARMS|Tracing Analysis|
|----------|----|----------------|
|Service positioning|ARMS is an APM service that supports application performance monitoring, user experience monitoring, tracing, and problem diagnostics.|Tracing Analysis is designed for distributed tracing.|
|Access method|Non-intrusive agent loading|Intrusive SDK programming|
|Billing method|Billed based on the number of agents, with competitive pricing|Billed based on the number of requests, with competitive pricing|
|Programming language|Java and PHP|Languages such as Java, PHP, Go, Python, JavaScript, .NET, and C++|
|Thread and memory diagnostics|Supported|Not supported|
|Local method stack|Supported|Not supported|

The following sections compare ARMS and Tracing Analysis in terms of the service positioning, access method, and billing method.

## Service positioning

ARMS is positioned as a heavyweight APM service that has rich features. You can install the ARMS agent for an application to access ARMS. The ARMS agent provides features such as performance monitoring, user experience monitoring, tracing, and fault diagnostics.

Tracing Analysis is designed to solve tracing problems in a distributed environment. You can implement distributed tracing by using Tracing Analysis SDK, which supports only trace monitoring.

## Access method

Positioned as an APM service, ARMS can be accessed in non-intrusive mode, which is popular among commercial APM tools. By using this mode, you do not need to modify the application code. You need only to install an agent for the application that you want to monitor, and modify the application startup mode. For example, when you use ARMS to monitor a Java application, you must add the -javaagent startup parameter during the application startup.

Positioned as a distributed tracing service, Tracing Analysis is based on open source products such as [Jaeger](https://github.com/jaegertracing/jaeger) and [Zipkin](https://github.com/openzipkin/zipkin), and the [OpenTracing](https://github.com/opentracing) open source standard. You can access Tracing Analysis by using an SDK based on Jaeger, Zipkin, or OpenTracing. This method brings the following benefits:

-   You can seamlessly migrate applications that use SDKs based on Jaeger, Zipkin, or OpenTracing to Tracing Analysis, without code modification.
-   You do not need to worry about vendor lock-in because Tracing Analysis SDK is based on an open source standard.
-   The community allows you to support a large number of programming languages at a time. This significantly reduces the threshold for access to trace monitoring when you develop applications in a heterogeneous environment.

## Billing method

Similar to other APM services, ARMS is billed based on the number of agents when you use features such as application monitoring and browser monitoring. The resulting fee may account for a large proportion of your budget. Based on a high-performance and efficient architecture, ARMS is billed at a rate that is only 10% to 20% of the industry average.

Designed for trace diagnostics in a distributed environment, Tracing Analysis is billed based on the number of requests, at a low rate.

## More information

Though ARMS and Tracing Analysis are differently positioned, both of them are monitoring services for development in Alibaba Cloud and will be interconnected in the future.

-   ARMS will support custom distributed tracing based on Tracing Analysis SDK.
-   Tracing Analysis will support queries in the ARMS console to improve your diagnostic experience.

**Related topics**  


[Tracing Analysis](https://www.alibabacloud.com/zh/products/tracing-analysis)

