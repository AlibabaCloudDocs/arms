# Differences between ARMS and Tracing Analysis

Both Application Real-Time Monitoring Service \(ARMS\) and Tracing Analysis can solve tracing problems in a distributed environment. This topic describes the differences between ARMS and Tracing Analysis.

## Background

ARMS is an application performance management \(APM\) product of Alibaba Cloud. With ARMS, you can quickly and conveniently build application monitoring capabilities with a response time within several seconds for businesses and enterprises based on custom dimensions such as the browser, application, and business.

Tracing Analysis provides a complete set of tools for distributed application development, including trace restoration, call statistics, trace topology, and application dependency analysis. Tracing Analysis helps you quickly analyze and diagnose performance bottlenecks in a distributed application architecture, improve the efficiency of microservice development and diagnosis, and reduce the costs of developing trace monitoring applications \(such as Jaeger and Zipkin\) and related storage services \(such as HBase and Elasticsearch\).

## Comparison between ARMS and Tracing Analysis

|Difference|ARMS|Tracing Analysis|
|----------|----|----------------|
|Product positioning|ARMS is an APM product that supports application performance monitoring, user experience monitoring, tracing, and problem diagnosis.|Tracing Analysis is designed for distributed tracing.|
|Access method|Non-intrusive agent loading|Intrusive SDK programming|
|Billing method|Billed based on the number of agents, with competitive pricing|Billed based on the number of requests, with competitive pricing|
|Programming language|Java and PHP|Java, PHP, Go, Python, JavaScript, .NET, and C++|
|Thread and memory diagnosis|Supported|Not supported|
|Local method stack|Supported|Not supported|

The following describes the differences between ARMS and Tracing Analysis in terms of the product positioning, access method, and billing method.

## Product positioning

ARMS is positioned as a heavyweight APM product with rich functions. Applications can access ARMS by installing an agent, which provides functions such as performance monitoring, user experience monitoring, tracing, and fault diagnosis.

Tracing Analysis is specifically designed to solve tracing problems in a distributed environment. You can implement distributed tracing through the Tracing Analysis SDK, which only supports trace monitoring.

## Access method

Positioned as an APM product, ARMS is accessed in non-intrusive mode, without code modification. You need to install an agent to the application you want to monitor and modify the application startup mode. For example, when you use ARMS to monitor a Java application, you need to add the -javaagent startup parameter during the application startup.

Positioned as a distributed tracing product, Tracing Analysis is based on open-source products [Jaeger](https://github.com/jaegertracing/jaeger) and [Zipkin](https://github.com/openzipkin/zipkin) and open-source standard [OpenTracing](https://github.com/opentracing). You can access Tracing Analysis by using an SDK based on Jaeger, Zipkin, or OpenTracing, with the following advantages:

-   You can seamlessly migrate applications that use SDKs based on Jaeger, Zipkin, or OpenTracing to Tracing Analysis, without code modification.
-   You do not need to worry about vendor lock-in because the Tracing Analysis SDK is based on open-source standards.
-   With the help of the community, you can support a large number of programming languages at a time, greatly simplifying trace monitoring during development in a heterogeneous environment.

## Billing method

Similar to other APM products, ARMS is billed based on the number of agents when you use functions such as application monitoring and browser monitoring. The resulting fee may account for a large proportion of your budget. Based on a high-performance and efficient architecture, ARMS is charged at a rate only 10% to 20% of the average rate of the industry.

Designed specifically for trace diagnosis in a distributed environment, Tracing Analysis is billed based on the number of requests, at a low rate.

## More information

Though positioned differently, both ARMS and Tracing Analysis are monitoring products for development in Alibaba Cloud and will be interconnected in the future.

-   ARMS will support custom distributed tracing based on the Tracing Analysis SDK.
-   Tracing Analysis will support queries in the ARMS console for optimized diagnosis experience.

**Related topics**  


[Tracing Analysis](https://www.alibabacloud.com/zh/products/tracing-analysis)

