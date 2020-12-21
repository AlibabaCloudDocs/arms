# Monitor applications other than Java and PHP applications

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

-   [t1134109.md\#](/intl.en-US/Setup/Integrate Go Application/Integrate your application with Tracing Analysis - Go.md)
-   [Report Go application data through Zipkin](/intl.en-US/Setup/Integrate Go Application/Report Go application data through Zipkin.md)
-   [t1134112.md\#]()
-   [Instrument Node. js applications](/intl.en-US/Setup/Start monitoring Node.js applications/Instrument Node. js applications.md)
-   [Use Jaeger to report .NET application data](/intl.en-US/Setup/Start monitoring .NET applications/Use Jaeger to report .NET application data.md)
-   [Use Zipkin to report .NET application data](/intl.en-US/Setup/Start monitoring .NET applications/Use Zipkin to report .NET application data.md)
-   [t1134119.md\#]()

## What to do next

After you complete the preparations, you can use the following features of Tracing Analysis:

-   View the key metrics of an application, such as the health score, number of requests today, and number of errors today. For more information, see [t1134121.md\#](/intl.en-US/Use the console/Application management/View application list.md).
-   View the key performance metrics and topology of an application. For more information, see [t1134122.md\#](/intl.en-US/Use the console/Application management/View application performance metrics and topology.md).
-   View the key performance metrics, call topology, and traces of an application on each host where the application is deployed. For more information, see [t1134123.md\#](/intl.en-US/Use the console/Application management/View application details.md).
-   View the API calls of an application. For more information, see [t1134124.md\#](/intl.en-US/Use the console/Application management/View interface invocation information.md).
-   Query traces by using the multi-dimensional query feature. For more information, see [t1134126.md\#](/intl.en-US/Use the console/Application management/Query invocation traces.md).
-   View the application traces, trace topologies, real-time aggregate trace tables, and waterfall plots of traces. For more information, see [Analyze traces](/intl.en-US/Use the console/Application management/Analyze traces.md).
-   Specify whether to display the host name and whether to collect application data, manage custom tags of an application, and delete an application. For more information, see [Manage applications and tags](/intl.en-US/Use the console/Application management/Manage applications and tags.md).

