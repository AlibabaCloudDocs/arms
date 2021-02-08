# What is Tracing Analysis?

Tracing Analysis provides a set of tools for you to develop distributed applications. These tools include trace mapping, call request statistics, trace topology, and application dependency analysis. You can use these tools to analyze and diagnose performance bottlenecks in a distributed application architecture and make microservice development and diagnostics more efficient.

## Architecture

The following figure shows the architecture of Tracing Analysis.

![Tracing Analysis Workflow](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/xtrace_dg_workflow.png "Architecture of Tracing Analysis")

Tracing Analysis works in the following process:

-   The applications of customers integrate the client SDKs of Tracing Analysis to report service call data. Tracing Analysis provides SDKs for a variety of languages. Tracing Analysis is compatible with SDKs from various open source communities and supports the OpenTracing standard.
-   After the data is reported to the Tracing Analysis console, Tracing Analysis aggregates and persists the data in real time to generate monitoring data. The monitoring data includes trace details, performance overview, and real-time topology. You can then troubleshoot and diagnose issues based on the monitoring data.
-   Tracing Analysis can send the trace data to downstream Alibaba Cloud services, such as LogSearch, Cloud Monitor, and MaxCompute. The data can be used in a variety of scenarios, such as offline analysis and alerting.

## Features

Tracing Analysis provides the following features:

-   Query and diagnostics of distributed traces: Tracing Analysis collects all user requests of microservices in a distributed architecture and summarizes these requests to distributed traces for query and diagnostics.
-   Real-time collection of application performance data: Tracing Analysis collects all user requests for an application and analyzes in real time the performance of the services and resources that constitute the application.
-   Dynamic discovery of distributed topologies: Tracing Analysis collects distributed call information for all your distributed microservices and relevant Platform as a Service \(PaaS\) products.
-   Program development in multiple languages: Tracing Analysis is fully compatible with services from open source communities such as Jaeger and Zipkin based on the OpenTracing standard.
-   Various downstream integration scenarios: Tracing Analysis provides traces that are immediately usable to Alibaba Cloud Log Service. Tracing Analysis can send the traces to downstream analysis platforms such as MaxCompute.

