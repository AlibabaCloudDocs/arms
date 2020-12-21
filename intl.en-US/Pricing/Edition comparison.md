# Edition comparison

Application Real-Time Monitoring Service \(ARMS\) includes multiple sub-services, such as Application Monitoring, Browser Monitoring, Prometheus Service, and Custom Monitoring. To meet different requirements, each sub-service provides multiple editions, including Beta Edition, Trial Edition, Pro Edition, and Platinum Edition. This topic compares the features of different editions for ARMS sub-services.

## Application Monitoring \(Java/PHP\)

ARMS Application Monitoring is an application performance monitoring tool. It combines the industry-leading theoretical models of distributed application monitoring and tracing with the practices of Alibaba Group. This sub-service provides more comprehensive, application-oriented, and real-time monitoring services.

Application Monitoring is available in the following editions:

-   Basic Edition:
    -   The Basic Edition provides a 15-day free trial. For more information about the free trial, see [15-day free trial of ARMS]().
    -   After you activate the Basic Edition, the trial quota is unavailable and the usage of resources is unlimited. If you want to use the pay-as-you-go billing method, you can upgrade the Basic Edition to the Pro Edition.
-   Pro Edition: Multiple enhanced features. After you activate the Pro Edition, the trial quota is unavailable and the usage of resources is unlimited. You can select the resource package or pay-as-you-go billing method.

|Features|Basic Edition|Pro Edition|
|--------|-------------|-----------|
|Application overview|
|[Overview](/intl.en-US/Application monitoring/Function specification/Application overview.md)

 Displays the statistics of applications such as the total number of requests, average response time, and number of real-time instances. It also displays time charts such as the number of service requests and the service response time. The application overview feature allows you to view the overall performance of the applications.![feature_pg_app_overview_tab_overview_analysis](../images/p141117.png)

|✔️|✔️|
|[Topology](/intl.en-US/Application monitoring/Function specification/Application overview.md)

Automatically identifies call relationships between applications or interfaces, and then generates a real-time topological graph.![feature_pg_app_overview_tab_topo](../images/p141119.png)

|❌|✔️|
|[3D topology](/intl.en-US/Application monitoring/Function specification/3D topology.md)

Displays the health status of applications, services, and hosts, and displays the upstream and downstream dependencies of the applications in three dimensions.![feature_pg_app_overview_tab_3dtopo](../images/p141121.png)

|❌|✔️|
|Application details|
|Overview

Automatically identifies call relationships between applications or interfaces, and then generates a real-time topological graph.![feature_pg_app_details_tab_topo](../images/p141122.png)

|❌|✔️|
|[JVM monitoring](/intl.en-US/Application monitoring/Function specification/Application details/JVM monitoring.md)

Monitors heap memory metrics, non-heap memory metrics, direct buffer metrics, memory-mapped buffer metrics, garbage collection \(GC\) details, and the number of JVM threads.![feature_pg_app_details_tab_jvm](../images/p141123.png)

|✔️|✔️|
|[Host monitoring](/intl.en-US/Application monitoring/Function specification/Application details/Host monitoring.md)

Monitors host metrics such as CPU, memory, disk, load, network traffic, and network packets.![feature_pg_app_details_tab_host](../images/p141125.png)

|✔️|✔️|
|[SQL analysis, NoSQL analysis, exception analysis, and error analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Displays and analyzes SQL statements, exceptions, and errors by application, instance, and API.![feature_pg_app_details_tab_sql](../images/p141126.png)

|❌|✔️|
|[Interface snapshot](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Displays interface snapshots by application, instance, and API.![feature_pg_app_details_tab_snapshot](../images/p141128.png)

|✔️|✔️|
|Interface invocation|
|Overview

Automatically identifies call relationships between applications or interfaces, and then generates a real-time topological graph. ![feature_pg_interface_calls_tab_topo](../images/p141129.png)

|❌|✔️|
|[SQL analysis and NoSQL analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Analyzes SQL statements by application, instance, and interface. This allows you to diagnose the causes of slow calls.![feature_pg_interface_calls_tab_sql](../images/p141130.png)

|❌|✔️|
|[Exception analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.mdsc_view_interface_exception)

Analyzes the drill-down information of exceptions by application, instance, and interface.![feature_pg_interface_calls_tab_exception](../images/p141132.png)

|❌|✔️|
|[Error analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.mdsc_view_interface_errors)

Displays the statistics of application errors and HTTP status codes.![feature_pg_interface_calls_tab_errors](../images/p141133.png)

|❌|✔️|
|[Upstream services and downstream services](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Displays the statistics of the APIs and their invocation performance metrics. The statistics include the number of requests, response time, and number of errors.![feature_pg_interface_calls_tab_upstream_downstream](../images/p141135.png)

|❌|✔️|
|[Interface snapshot](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Displays interface snapshots by application, instance, and API.![feature_pg_interface_calls_tab_snapshot](../images/p141136.png)

|✔️|✔️|
|Event centerManages, stores, analyzes, and displays event data that is generated by cloud services in a unified manner.

|✔️|✔️|
|Database invocation|
|Overview

Automatically identifies call relationships between applications and databases, and then generates a real-time topological graph. ![feature_pg_db_calls_tab_topo](../images/p141137.png)

|❌|✔️|
|[SQL analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Analyzes SQL statements by application, instance, and interface. This allows you to diagnose the causes of slow calls.![feature_pg_db_calls_tab_sql](../images/p141138.png)

|✔️|✔️|
|[Exception analysis](/intl.en-US/Application monitoring/Function specification/API call monitoring.mdsc_view_interface_exception)

Analyzes the drill-down information of exceptions by application, instance, and interface.![feature_pg_db_calls_tab_exception.](../images/p141140.png)

|❌|✔️|
|Call sourceDisplays the interfaces through which databases are called.

![ Call source](../images/p173058.png)

|✔️|✔️|
|[Interface snapshot](/intl.en-US/Application monitoring/Function specification/API call monitoring.md)

Displays interface snapshots by application, instance, and API.![feature_pg_db_calls_tab_snapshot](../images/p141143.png)

|✔️|✔️|
|Other monitoring features|
|External calls

Displays the statistics of metrics, such as the number of external requests, response time, number of errors, and HTTP status codes.![feature_pg_external_calls](../images/p141175.png)

|✔️|✔️|
|[MQ monitoring](/intl.en-US/Application monitoring/Function specification/MQ monitoring.md)

Displays the status of the topic publishing and subscription of Message Queue for Apache RocketMQ.![feature_pg_mq_monitoring.png](../images/p141176.png)

|❌|✔️|
|Application diagnosis|
|[Real-time diagnostics](/intl.en-US/Application monitoring/Function specification/Application diagnosis/Real-time diagnosis.md)

After the real-time diagnosis feature is enabled, Application Monitoring continuously monitors the application for 5 minutes. Then, it provides reports for all trace data during this period.![feature_pg_realtime_diagnosis.png](../images/p141178.png)

|❌|✔️|
|Exception diagnosis

Displays the number of times, name, interface, and summary of all exceptions in an aggregated manner.![feature_pg_exception_analysis](../images/p141181.png)

|✔️|✔️|
|[Thread profiling]()

Displays the statistics of CPU time consumption by thread and the number of threads for each type. This feature records and aggregates method stacks of threads every 5 minutes to simulate the code execution process.![feature_pg_thread_profiling](../images/p141183.png)

|❌|✔️|
|Application settings|
|[Install the agent and delete applications](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md)

Multiple methods to install the agent are supported. Applications can be deleted with one click.![feature_pg_app_settings_agent](../images/p141184.png)

|✔️|✔️|
|[Modify the settings of sampling rate of invocation traces and agent switch](/intl.en-US/Application monitoring/Function specification/Application Settings/Custom configuration.md)

You can set the sampling rate of invocation traces, agent switch, thresholds, and filtering rules for invalid interface invocations.![feature_pg_app_settings_custom_configs](../images/p141185.png)

|❌|✔️|
|Trace query|
|[Query distributed trace and local method stack](/intl.en-US/Application monitoring/Function specification/Trace query.md)

You can query and view the distributed trace and local call method stack by call type, response time, application name, IP address, and API.|✔️|✔️|
|[Holographic troubleshooting]()

Displays trace IDs and traces.|✔️|✔️|
|Alerts and dashboards|
|[Create an alert](/intl.en-US/Quick start/Quickly create ARMS alerts.md)

You can configure alert rules based on the metrics of application monitoring.|✔️|✔️|
|[Create a dashboard](/intl.en-US/Quick start/Create a dashboard for an application monitoring job.md)

You can configure dashboards based on specific requirements for application monitoring.|❌|✔️|
|Supported agents|
|[Support multiple third-party Java components and frameworks](/intl.en-US/Application monitoring/Overview.md)

Supports Tomcat, Jetty, Spring Boot, Dubbo, HSF, HttpClient, MySQL, Oracle, and all Alibaba Cloud middleware services.|✔️|✔️|
|API operations|
|[List of API operations by feature](/intl.en-US/API reference/API overview.md)

You can obtain the results of application monitoring by calling the related API operations of ARMS Application Monitoring.|✔️|✔️|
|Retention policy for monitoring data|
|The retention period of metric data: the retention period of time series data that is generated when you call applications to perform query and statistical operations. In this case, the time series data includes transactions per second \(TPS\) and response time.|3 days|60 days|
|The retention period of tracing data: the retention period of detailed data that is generated when you call applications to perform query and diagnosis operations. In this case, the detailed data includes distributed call stacks.|1 day|30 days|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms_app_post#/buy)|

## Browser Monitoring

ARMS Browser Monitoring monitors experience data to check the health status of web pages in the following three aspects: page loading speed \(speed test\), page stability \(JavaScript errors\), and the success rate of external service calling \(API\).

Browser Monitoring is available in the following editions:

-   Basic Edition:
    -   The Basic Edition provides a free trial. For more information about the free trial, see [15-day free trial of ARMS]().
    -   After you activate the Basic Edition, the trial quota is unavailable and the usage of resources is unlimited. If you want to use the pay-as-you-go billing method, you can upgrade the Basic Edition to the Pro Edition.
-   Pro Edition: Multiple enhanced features. After you activate the Pro Edition, the trial quota is unavailable and the usage of resources is unlimited. You can select the resource package or pay-as-you-go billing method.

|Features|Basic Edition|Pro Edition|
|--------|-------------|-----------|
|Applications|
|[Overview](/intl.en-US/Browser monitoring/Overview.md)

Displays the statistics of metrics, such as the satisfaction rate, JavaScript \(JS\) error rate, page speed, and API request success rate.|✔️|✔️|
|[Satisfaction trend](/intl.en-US/Browser monitoring/Statistical metrics.md)

Displays the satisfaction trend \(APDEX trend\) by time and page.|❌|✔️|
|[Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)

Displays the page speed by time and page.|✔️**Note:** The Basic Edition does not support Slow Page Session Trace \(TOP20\).

|✔️|
|[Session tracing]()

Performs end-to-end tracing by username or user ID. It can also be used to trace the user behavior.|❌|✔️|
|[JS error diagnosis](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md)

Displays the JS stability metrics, such as Page Ranked by Error Rate, Frequent Errors, and Error View.|✔️**Note:** The Basic Edition does not support View Session.

|✔️|
|[API request](/intl.en-US/Browser monitoring/Console functions/API request monitoring.md)

Displays the API request metrics, such as the API success rate, API response time, and API response information.|✔️|✔️|
|[API details]()

Displays all the API request statistics of the application in a specified period. The statistics include the success rate, average success response time, average failure response time, number of slow responses, and number of errors.|✔️**Note:** The Basic Edition does not support View Session.

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
|PageDisplays the views ranking by page.

|✔️**Note:** The Basic Edition does not support View Session.

|✔️|
|Geographical viewDisplays the views ranking by location.

|✔️|✔️|
|Terminal detailsDisplays the views ranking by operating system, device, browser, and resolution.

|✔️|✔️|
|Network detailsDisplays the views ranking by carrier and connection type.

|✔️|✔️|
|Settings|
|Alarm ManagementYou can configure alert rules by actual conditions of the current website.

|✔️|✔️|
|[Application settings](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md)

You can modify the settings such as automatic API reporting, automatic SPA parsing, data collection of First Meaning Paint \(FMP\), and page resource reporting.|✔️|✔️|
|Issue location service|
|Troubleshoot application issues based on reverse data drilling.

Displays the access speed of applications, JS stability, and success rate of API requests. The statistics are based on dimensions such as Chinese provinces and cities, countries, operating systems, devices, browsers, resolutions, carriers, and connection types.|✔️|✔️|
|Access query

Displays raw access logs that are reported by all agents.|✔️|✔️|
|Open data service|
|Open datasets

Allows you to call the datasets of raw access logs.|✔️|✔️|
|[API reference](/intl.en-US/Browser monitoring/Methods user guide.md)

You can query the statistical results of all browser monitoring datasets by calling related API operations.|✔️|✔️|
|Alerts and dashboards|
|[Create an alert](/intl.en-US/Quick start/Quickly create ARMS alerts.md)

You can configure alert rules based on the metrics of application monitoring.|❌|✔️|
|[Create a dashboard](/intl.en-US/Dashboard and alarm/Create an interactive dashboard.md)

You can configure dashboards based on specific requirements for application monitoring.|❌|✔️|
|Page views \(PVs\) of websites|
|The limit on the PVs of frontend websites is supported.

The daily usage is calculated and limited based on the total number of PVs of all websites. Different editions support different specifications.|Unlimited. The pay-as-you-go billing method is used.|Unlimited. The pay-as-you-go billing method is used.|
|Retention policy for monitoring data|
|Sampling rate of detailed invocation data to be retained

The sampling rate of detailed website invocation request data to be retained.|10%|10%|
|Retention period of statistical aggregate data

The retention period of time series data that is generated when you call applications to perform query and statistical operations. In this case, the time series data includes PVs and unique visitors \(UVs\).|3 days|60 days|
|Retention period of detailed diagnosis data

The retention period of detailed data that is generated when you call operations to perform query and diagnosis operations. In this case, the detailed data includes call URLs and headers.|3 days|30 days|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms_web_post#/buy)|

## Prometheus Service

Prometheus Service supports the open source Prometheus ecosystem and monitors multiple components. It provides out-of-the-box monitoring dashboards and fully managed Prometheus services.

Prometheus Service is available only in the Trial Edition. It is valid until 00:00 on the 15th day after Prometheus Service is activated. During this period, two million custom metrics can be reported free of charge every day.

**Note:** The size of each reported metric cannot exceed 2 KB. Each metric is stored for up to 15 days. The data metrics that are stored for more than 15 days are deleted.

|Edition|Trial Edition|
|-------|-------------|
|Interface-based installation of third-party exporters|✔️|
|Service discovery of ServiceMonitor|✔️|
|Custom configurations of Prometheus services|✔️|
|Data storage on the cloud|30 days|
|Out-of-the-box Grafana dashboard|✔️|
|Custom Grafana dashboard|❌|
|PromQL supported|❌|
|Alerts|✔️|
|Activation link|[Activate now](https://common-buy.aliyun.com/?commodityCode=arms#/open)|

## References

For information about the pay-as-you-go billing method and the pricing of resource packages of ARMS on the China site \(aliyun.com\) and International site \(alibabacloud.com\), see [ARMS pricing](https://www.aliyun.com/price/product?#/arms/detail).



