# Edition comparison

Application Real-Time Monitoring Service \(ARMS\) includes multiple sub-services, such as Application Monitoring, Browser Monitoring, Prometheus Monitoring, and Custom Monitoring. To meet different requirements, each sub-service provides multiple editions, such as the Public Preview Edition, Trial Edition, Pro Edition, and Platinum Edition. This topic compares the features of different editions of ARMS sub-services.

## Application Monitoring \(Java/PHP\)

ARMS Application Monitoring is an application performance monitoring tool. It combines the industry-leading theoretical models of distributed application monitoring and tracing with the practices of Alibaba Group. This sub-service provides more comprehensive, application-oriented, and real-time monitoring services.

Application Monitoring is available in the following editions:

-   Basic Edition:

    -   The Basic Edition provides a 15-day free trial. For more information about the free trial, see [15-day free trial of ARMS](/intl.en-US/Billing/15-day free trial of ARMS.md).
    -   After you activate the Basic Edition, the trial quota is unavailable and the usage of resources is unlimited. If you want to use the pay-as-you-go billing method, you can upgrade the Basic Edition to the Pro Edition.
    **Note:** The Basic Edition does not support deduction of resource plans.

-   Pro Edition: This edition has multiple enhanced features. After you activate the Pro Edition, the trial quota is unavailable and the usage of resources is unlimited. You can select the resource plan or pay-as-you-go billing method.

|Feature|Basic Edition|Pro Edition|
|-------|-------------|-----------|
|Application overview|
|[Overview](/intl.en-US/Application monitoring/Console functions/Application overview.md)

 Displays the statistics of applications such as the total number of requests, average response time, and number of real-time instances. It also displays time charts such as the number of service requests and the service response time. The application overview feature allows you to view the overall performance of the applications.![feature_pg_app_overview_tab_overview_analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141117.png)

|✔️|✔️|
|[Topology](/intl.en-US/Application monitoring/Console functions/Application overview.md)

Automatically identifies call relationships between applications or APIs, and generates a real-time topological graph.![feature_pg_app_overview_tab_topo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141119.png)

|❌|✔️|
|[3D topology](/intl.en-US/Application monitoring/Console functions/3D topology.md)

Displays the health status of applications, services, and hosts, and displays the upstream and downstream dependencies of the applications.![feature_pg_app_overview_tab_3dtopo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141121.png)

|❌|✔️|
|Application details|
|Overview

Automatically identifies call relationships between applications or APIs, and generates a real-time topological graph.![feature_pg_app_details_tab_topo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141122.png)

|❌|✔️|
|[JVM monitoring](/intl.en-US/Application monitoring/Console functions/Application details/JVM monitoring.md)

Monitors heap memory metrics, non-heap memory metrics, direct buffer metrics, memory-mapped buffer metrics, garbage collection \(GC\) details, and the number of JVM threads.![feature_pg_app_details_tab_jvm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141123.png)

|✔️|✔️|
|[Host monitoring](/intl.en-US/Application monitoring/Console functions/Application details/Host monitoring.md)

Monitors host metrics such as CPU, memory, disk, load, network traffic, and network packets.![feature_pg_app_details_tab_host](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141125.png)

|✔️|✔️|
|[SQL analysis, NoSQL analysis, exception analysis, and error analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Displays and analyzes SQL statements, exceptions, and errors in different dimensions such as the application, instance, and API.![feature_pg_app_details_tab_sql](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141126.png)

|❌|✔️|
|[API snapshots](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Displays API snapshots in different dimensions such as the application, instance, and API.![feature_pg_app_details_tab_snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547484161/p141128.png)

|✔️|✔️|
|API invocation|
|Overview

Automatically identifies call relationships between applications or APIs, and generates a real-time topological graph. ![feature_pg_interface_calls_tab_topo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8547484161/p141129.png)

|❌|✔️|
|[SQL analysis and NoSQL analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Analyzes SQL statements in different dimensions such as the application, instance, and API. This allows you to diagnose the causes of slow calls.![feature_pg_interface_calls_tab_sql](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8547484161/p141130.png)

|❌|✔️|
|[Exception analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.mdsc_view_interface_exception)

Analyzes the drill-down information of exceptions in different dimensions such as the application, instance, and API.![feature_pg_interface_calls_tab_exception](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8547484161/p141132.png)

|❌|✔️|
|[Error analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.mdsc_view_interface_errors)

Displays the statistics of application errors and HTTP status codes.![feature_pg_interface_calls_tab_errors](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8547484161/p141133.png)

|❌|✔️|
|[Upstream services and downstream services](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Displays the statistics of the APIs and their invocation performance metrics. The statistics include the number of requests, response time, and number of errors.![ARMS Application Monitoring - Interface Invocation - Upstream Services](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3761458061/p64182.png)

|❌|✔️|
|[API snapshots](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Displays API snapshots in different dimensions such as the application, instance, and API.![feature_pg_interface_calls_tab_snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8547484161/p141136.png)

|✔️|✔️|
|Event centerManages, stores, analyzes, and displays event data that is generated by cloud services in a unified manner.

|✔️|✔️|
|Database invocation|
|Overview

Automatically identifies call relationships between applications and databases, and generates a real-time topological graph. ![Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2534424161/p235853.png)

|❌|✔️|
|[SQL analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Analyzes SQL statements in different dimensions such as the application, instance, and API. This allows you to diagnose the causes of slow calls.![SQL Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236052.png)

|✔️|✔️|
|[Exception analysis](/intl.en-US/Application monitoring/Console functions/API monitoring.mdsc_view_interface_exception)

Analyzes the drill-down information of exceptions in different dimensions such as the application, instance, and API.![Exception Analysis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236127.png)

|❌|✔️|
|Call sourceDisplays the APIs that are used to call databases.

![Call source](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236346.png)

|✔️|✔️|
|[API snapshots](/intl.en-US/Application monitoring/Console functions/API monitoring.md)

Displays API snapshots in different dimensions such as the application, instance, and API.![Interface Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3534424161/p236484.png)

|✔️|✔️|
|Other monitoring features|
|External calls

Displays the statistics of metrics, such as the number of external requests, response time, number of errors, and HTTP status codes.![External call overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3394658061/p185227.png)

|✔️|✔️|
|[MQ monitoring](/intl.en-US/Application monitoring/Console functions/MQ monitoring.md)

Displays the status of the topic publishing and subscription of Message Queue for Apache RocketMQ.|❌|✔️|
|Application diagnosis|
|[Real-time diagnostics](/intl.en-US/Application monitoring/Console functions/Application diagnosis/Real-time diagnostics.md)

After the real-time diagnosis feature is enabled, Application Monitoring continuously monitors the application for 5 minutes. Then, it provides reports for all trace data during this period.![Page Realtime Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8732728061/p54055.png)

|❌|✔️|
|Exception analysis

Displays the number of occurrences, name, related API, and summary of each exception in an aggregated manner.|✔️|✔️|
|[Thread profiling](/intl.en-US/Application monitoring/Console functions/Application diagnosis/Thread profiling.md)

Displays the thread-specific statistics of CPU time consumption and the number of threads for each type. This feature records and aggregates method stacks of threads every 5 minutes to simulate the code execution process.![pg_am_threads_profiling](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5289262851/p82887.png)

|❌|✔️|
|Application settings|
|[Install the agent and delete applications](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md)

Multiple methods to install the agent are supported. Applications can be deleted with one click.|✔️|✔️|
|[Modify the settings of the sampling rate of invocation traces and the agent switch](/intl.en-US/Application monitoring/Console functions/Application Settings/Custom configuration.md)

You can set the sampling rate of invocation traces, agent switch, thresholds, and filtering rules for invalid API invocations.|❌|✔️|
|Trace query|
|[Query distributed traces and local method stacks](/intl.en-US/Application monitoring/Console functions/Trace query.md)

You can query and view the distributed trace and local call method stack in different dimensions such as the call type, response time, application name, IP address, and API.|✔️|✔️|
|Alerts and dashboards|
|[Create an alert](/intl.en-US/Quick start/Create ARMS alerts.md)

You can configure alert rules based on the metrics of application monitoring.|✔️|✔️|
|[Create an interactive dashboard](/intl.en-US/Quick start/Create a dashboard for an application monitoring job.md)

You can configure interactive dashboards based on specific requirements for application monitoring.|❌|✔️|
|Supported agents|
|[Support multiple third-party Java components and frameworks](/intl.en-US/Application monitoring/Overview.md)

Supports Tomcat, Jetty, Spring Boot, Dubbo, High-Speed Service Framework \(HSF\), HttpClient, MySQL, Oracle, and all Alibaba Cloud middleware services.|✔️|✔️|
|API operations|
|[List of operations by function](/intl.en-US/API reference/API Overview.md)

You can obtain the results of application monitoring by calling the related API operations of ARMS Application Monitoring.|✔️|✔️|
|Retention policy for monitoring data|
|The retention period of metric data indicates the retention period of time series data that is generated when you call applications to perform query and statistical operations. In this case, the time series data includes transactions per second \(TPS\) and response time.|3 days|60 days|
|The retention period of tracing data indicates the retention period of detailed data that is generated when you call applications to perform query and diagnostic operations. In this case, the detailed data includes distributed call stacks.|1 day|30 days|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms_app_post#/buy)|

## Browser Monitoring

ARMS Browser Monitoring monitors experience data to check the health status of web pages in the following three aspects: page loading speed \(speed test\), page stability \(JavaScript errors\), and the success rate of calls to external services \(APIs\).

Browser Monitoring is available in the following editions:

-   Basic Edition:

    -   The Basic Edition provides a free trial. For more information about the free trial, see [15-day free trial of ARMS](/intl.en-US/Billing/15-day free trial of ARMS.md).
    -   After you activate the Basic Edition, the trial quota is unavailable and the usage of resources is unlimited. If you want to use the pay-as-you-go billing method, you can upgrade the Basic Edition to the Pro Edition.
    **Note:** The Basic Edition does not support deduction of resource plans.

-   Pro Edition: This edition has multiple enhanced features. After you activate the Pro Edition, the trial quota is unavailable and the usage of resources is unlimited. You can select the resource plan or pay-as-you-go billing method.

|Feature|Basic Edition|Pro Edition|
|-------|-------------|-----------|
|Applications|
|[Overview](/intl.en-US/Browser monitoring/What is ARMS Browser Monitoring?.md)

Displays the statistics of metrics, such as the satisfaction rate, JS error rate, page speed, and success rate of API requests.|✔️|✔️|
|[Satisfaction trend](/intl.en-US/Browser monitoring/Statistical metrics.md)

Displays the Apdex-based satisfaction trend by time and page.|❌|✔️|
|[Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)

Displays the page speed by time and page.|✔️**Note:** The Basic Edition does not support Slow Page Session Trace \(TOP20\).

|✔️|
|[Session tracing](/intl.en-US/Browser monitoring/Console functions/Session tracing.md)

Performs end-to-end tracing based on the username or user ID. It can also be used to trace user behaviors.|❌|✔️|
|[JS error diagnostics](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md)

Displays the JS stability metrics, such as Page Ranked by Error Rate, Frequent Errors, and Error View.|✔️**Note:** The Basic Edition does not support View Session.

|✔️|
|[API request](/intl.en-US/Browser monitoring/Console functions/API request.md)

Displays the API request metrics, such as the success rate of API requests, API response time, and API response information.|✔️|✔️|
|[API details](/intl.en-US/Browser monitoring/Console functions/API details.md)

Displays all the API request statistics of the application in a specified period. The statistics include the success rate of API requests, average success response time, average failure response time, number of slow responses, and number of errors.|✔️**Note:** The Basic Edition does not support View Session.

|✔️|
|[Custom statistics](/intl.en-US/Browser monitoring/Console functions/Custom statistics.md)

Supports the following two custom statistics features: SUM log and AVG log.|✔️|✔️|
|View details

Displays the statistics and distribution of the manually reported SUM log and AVG log.|✔️**Note:** The Basic Edition does not support View Session or Aggregation Dimensions.

|✔️|
|Multi-dimensional analysis

You can view multiple types of logs based on different conditions.|❌|✔️|
|Dimensions

️|
|PageDisplays the ranking of views by page.

|✔️**Note:** The Basic Edition does not support View Session.

|✔️|
|Geographical viewDisplays the ranking of views by location.

|✔️|✔️|
|Terminal detailsDisplays the ranking of views in these dimensions: the operating system, device, browser, and resolution.

|✔️|✔️|
|Network detailsDisplays the ranking of views by carrier and connection type.

|✔️|✔️|
|Settings|
|Alert managementYou can configure alert rules based on actual conditions of the current website.

|✔️|✔️|
|[Application settings](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md)

You can modify the settings such as automatic reporting of the API call success rate, automatic SPA page resolution, data collection of First Meaning Paint \(FMP\), and page resource reporting.|✔️|✔️|
|Issue location service|
|Troubleshoot application issues based on reverse data drilling.

Displays the access speed of applications, JS stability, and success rate of API requests. The statistics are based on dimensions such as Chinese provinces and cities, countries and regions, operating systems, devices, browsers, resolutions, carriers, and connection types.|✔️|✔️|
|Access query

Displays raw access logs that are reported by all agents.|✔️|✔️|
|Open data service|
|Open datasets

Allows you to call the datasets of raw access logs.|✔️|✔️|
|[API reference](/intl.en-US/Browser monitoring/API reference.md)

You can query the statistical results of all Browser Monitoring datasets by calling related API operations.|✔️|✔️|
|Alerts and dashboards|
|[Create an alert](/intl.en-US/Quick start/Create ARMS alerts.md)

You can configure alert rules based on the metrics of Browser Monitoring.|❌|✔️|
|[Create an interactive dashboard](/intl.en-US/Dashboard and alerting/Create a dashboard.md)

You can configure dashboards based on specific requirements for Browser Monitoring.|❌|✔️|
|Page views \(PVs\) of websites|
|The limit on the PVs of frontend websites is supported.

The daily usage is calculated and limited based on the total number of PVs of all websites. Different editions support different specifications.|Unlimited. The pay-as-you-go billing method is used.|Unlimited. The pay-as-you-go billing method is used.|
|Retention policy for monitoring data|
|Sampling rate of detailed invocation data to be retained

The sampling rate of detailed website invocation request data to be retained.|10%|10%|
|Retention period of statistical aggregate data

The retention period of time series data that is generated when you call applications to perform query and statistical operations. In this case, the time series data includes PVs and unique visitors \(UVs\).|3 days|60 days|
|Retention period of detailed diagnosis data

The retention period of detailed data that is generated when you call operations to perform query and diagnostic operations. In this case, the detailed data includes call URLs and headers.|3 days|30 days|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms_web_post#/buy)|

## Prometheus Monitoring

Prometheus Monitoring is a managed monitoring service of ARMS. Prometheus Monitoring is compatible with the open source Prometheus ecosystem. Prometheus Monitoring monitors a wide variety of components and provides various out-of-the-box dashboards.

Prometheus Monitoring is available only in the Trial Edition. It is valid until 00:00 on the 15th day after Prometheus Monitoring is activated. During this period, 2 million custom metrics can be reported for free every day.

**Note:** The size of each reported metric cannot exceed 2 KB. Each metric is stored for up to 15 days. The data metrics that are stored for more than 15 days are deleted.

|Edition|Trial Edition|
|-------|-------------|
|Interface-based installation of third-party exporters|✔️|
|Service discovery of ServiceMonitor|✔️|
|Custom configurations of Prometheus Monitoring|✔️|
|Data storage on the cloud|30 days|
|Out-of-the-box Grafana dashboard|✔️|
|Custom Grafana dashboard|❌|
|Support for PromQL|❌|
|Alert|✔️|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|

## References

For more information about the pay-as-you-go billing method and the pricing of resource plans of ARMS on the China site \(aliyun.com\) and International site \(alibabacloud.com\), see [ARMS Pricing](https://www.aliyun.com/price/product?#/arms/detail).



