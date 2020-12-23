# What is Tracing Analysis?

Tracing Analysis provides a variety of tools for distributed applications, including trace mapping, request counting, trace topology, and application dependency Analysis. With these tools, developers can quickly identify the performance bottlenecks of a distributed application architecture and improve the efficiency of microservice development and diagnosis.

## Architecture

The following figure shows the product architecture of link tracing.

![Tracing Analysis Workflow](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/xtrace_dg_workflow.png "Product Architecture of tracing analysis")

The main work process is as follows:

-   The customer application reports service calls through the integrated tracing analysis SDK. Tracing analysis supports SDKs from various open source communities and the OpenTracing standard.
-   After the tracing data is reported to the tracing analysis console, the tracing analysis component aggregates, computes, and persists the data in real time to form monitoring data such as the trace details, Performance Overview, and real-time topology data. You can then troubleshoot and diagnose the problem.
-   You can use the trace data to connect to downstream Alibaba cloud products, such as LogSearch, CloudMonitor, and MaxCompute, for offline analysis and alert management.

## Features

The main features of link tracing include:

-   Query and diagnostics of distributed traces: This feature tracks microservice user requests in the distributed architecture and summarizes these requests into distributed traces.
-   Real-time collection of application performance data: This feature tracks all user requests for an application and collects and analyzes in real time the performance data of the services and resources that constitute the application.
-   Dynamic Discovery of distributed topology: In this way, you can obtain the distributed call information collected by tracing analysis for your distributed micro-application and PaaS products.
-   Programming for multiple languages: This service is based on OpenTracing and fully compatible with open-source communities such as Jaeger and Zipkin.
-   Various downstream integration scenarios: uses collected traces for log analysis and connects to downstream analysis platforms such as MaxCompute.

