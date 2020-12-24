# Monitor other applications

Application Real-Time Monitoring Service \(ARMS\) can monitor Java and PHP applications. Tracing Analysis can be used to monitor applications written in other programming languages such as C++, Go, Node.js, and NET. After you prepare for application monitoring, Tracing Analysis can provide features such as query and diagnostics of distributed traces, real-time integration of performance data, and dynamic discovery of distributed topologies. These features can help you monitor applications.

## Background information

Tracing Analysis provides a set of tools for distributed application development. These tools include trace mapping, call request statistics, trace topology, and application dependency analysis. You can use these tools to analyze and diagnose performance bottlenecks in a distributed application architecture and make microservice development and diagnostics more efficient. Tracing Analysis provides the following features:

-   Query and diagnostics of distributed traces: This feature tracks microservice user requests in the distributed architecture and summarizes these requests into distributed traces.
-   Real-time collection of application performance data: This feature tracks all user requests for an application and collects and analyzes in real time the performance data of the services and resources that constitute the application.
-   Dynamic discovery of distributed topologies: This feature collects information about distributed calls to your distributed microservice applications and Platform as a Service \(PaaS\) products.
-   Multi-language development program: Tracing Analysis is fully compatible with open source communities such as Jaeger and Zipkin based on the OpenTracing standard.
-   Integration with various downstream analysis platforms: This feature uses collected traces for log analysis and allows Tracing Analysis to connect to downstream analysis platforms such as MaxCompute.

## Monitor multi-language applications

Check documents based on the language of your application.

-   [Integrate your application with Tracing Analysis - Go](/intl.en-US/Preparations/Start monitoring Go applications/Use Jaeger to report Go application data.md)
-   [Report Go application data through Zipkin](/intl.en-US/Preparations/Start monitoring Go applications/Report Go application data through Zipkin.md)
-   [Integrate your application with Tracing Analysis - Python](/intl.en-US/Preparations/Start monitoring Python applications/Use Jaeger to report Python application data.md)
-   [Access Node.js applications](/intl.en-US/Preparations/Start monitoring Node.js applications/Access Node.js applications.md)
-   [Use Jaeger to report data of. NET applications](/intl.en-US/Preparations/Start monitoring .NET applications/Use Jaeger to report data of. NET applications.md)
-   [Logs of. NET applications are reported through Zipkin.](/intl.en-US/Preparations/Start monitoring .NET applications/Logs of. NET applications are reported through Zipkin..md)
-   [Integrate your application with Tracing Analysis - C++](/intl.en-US/Preparations/Monitor C ++ applications/Use Jaeger to report data of C ++ applications.md)

## What to do next

After you complete the preparations, you can use the following features of Tracing Analysis:

-   View the key metrics of an application, such as the health score, number of requests today, and number of errors today. For more information, see [View application list](/intl.en-US/Console guide/Application management/View applications.md).
-   View the key performance metrics and topology of an application. For more information, see [View application performance metrics and topology](/intl.en-US/Console guide/Application management/View key application performance metrics and topology.md).
-   View the key performance metrics, call topology, and traces of an application on each host where the application is deployed. For more information, see [View application details](/intl.en-US/Console guide/Application management/View application details.md).
-   View the API calls of an application. For more information, see [View interface invocation information](/intl.en-US/Console guide/Application management/View API usage.md).
-   Query traces by using the multi-dimensional query feature. For more information, see [Query invocation traces](/intl.en-US/Console guide/Application management/Query trace.md).
-   View the application traces, trace topologies, real-time aggregate trace tables, and waterfall plots of traces. For more information, see [Analyze a trace](/intl.en-US/Console guide/Application management/Analyze a trace.md).
-   Specify whether to display the host name and whether to collect application data, manage custom tags of an application, and delete an application. For more information, see [Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md).

