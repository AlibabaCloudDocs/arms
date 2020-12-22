# Release notes

This topic provides the release notes of Application Real-Time Monitoring Service \(ARMS\) and new features of each version.

## V2.7.8

**Release date: November 8, 2020**

**New features:**

-   SLO
    -   SLO is supported.

## V2.7.7.1

**Release date: November 3, 2020**

**New features:**

-   Synthetic monitoring
    -   Synthetic monitoring recorder is supported.
    -   Recording script via the Chrome browser is supported.

## V2.7.7

**Release date: October 15, 2020**

**New features:**

-   Synthetic monitoring
    -   Synthetic monitoring v0.1 is supported.
    -   Scheduled synthetic monitoring by city, carrier, and network is supported.

## V2.7.6.2

**Release date: September 15, 2020**

**New features:**

-   Dashboard and alerting
    -   Metrics support dynamic baseline.

## V2.7.5.3

**Release date: August 20, 2020**

**New features:**

-   Application monitoring
    -   Node.js monitoring is supported.

## V2.7.4.1

**Release date: August 3, 2020**

**New features:**

-   Application monitoring
    -   AIOps automatic diagnosis supports business impact evaluation.

## V2.7.3

**Release date: July 9, 2020**

**New features:**

-   Prometheus monitoring
    -   Function Compute monitoring is supported.

## V2.7.2

**Release date: June 5, 2020**

**New features:**

-   Prometheus monitoring
    -   Self-host Kubernetes monitoring is supported.

## V2.7.1

**Release date: May 15, 2020**

**New features:**

-   Prometheus monitoring
    -   Blackbox-based VPC inspection is supported.

## V2.7.0

**Release date: April 2, 2020**

**New features:**

-   Application monitoring
    -   Automatic analysis of trace performance problem is supported.

## V2.6.5

**Release date: March 5, 2020**

**New features:**

-   Browser monitoring
    -   Multi-dimensional query of performance metrics is supported.

## V2.6.2

**Release date: February 14, 2020**

**New features:**

-   Application monitoring
    -   Business transaction is supported.
    -   The WebFlux and Gateway components of Spring Cloud are supported.

## V2.6.1

**Release date: February 11, 2020**

**New features:**

-   Application monitoring
    -   Metadata of microservices can be obtained.

## V2.6.0.2

**Release date: January 2, 2020**

**New features:**

-   Application monitoring
    -   Exception diagnosis is supported.

**Optimized features:**

-   Application monitoring
    -   Bugs of the Thrift plug-in are fixed.

## V2.6.0

**Release date: December 17, 2019**

**New features:**

-   Application monitoring
    -   Asynchronous invocation is supported.
    -   Parameters called by Dubbo and HSFProvider can be recorded.

## V2.5.9.5

**Release date: November 28, 2019**

**New features:**

-   Application monitoring
    -   The JFinal-Undertow plug-in is supported.

**Optimized features:**

-   Application monitoring
    -   Bugs are fixed. Thread profiling data of Dubbo can be obtained.

## V2.5.9.3

**Release date: November 25, 2019**

**New features:**

-   Application monitoring
    -   ARMS can be integrated with Tracing Analysis.

## V2.5.9

**Release date: September 6, 2019**

**Optimized features:**

-   Application monitoring
    -   The denial-of-service \(DoS\) vulnerability of Fastjson is fixed.
    -   The logic used to obtain the IP address of the network card is modified.

## V2.5.8

**Release date: August 2, 2019**

**New features:**

-   Application monitoring
    -   The dual-state alerting feature is supported. This allows you to configure alert rules for metrics that have only two states: yes or no.
    -   The plug-in of DM databases is supported.

## V2.5.7.2

**Release date: July 30, 2019**

**New features:**

-   Application monitoring
    -   Metrics of JVM Metaspace are supported.
    -   HTTP status codes that are not counted as errors can be customized. By default, HTTP status codes greater than 400 are counted as errors. You can also customize HTTP status codes that are greater than 400 but not counted as errors. For more information, see [Configure advanced settings](/intl.en-US/Application monitoring/Features provided by the console/Application Settings/Custom configuration.mdsc_advanced_options).

## V2.5.7

**Release date: July 11, 2019**

**Optimized features:**

-   Application monitoring
    -   Fastjson is upgraded to fix security vulnerabilities.

## V2.5.6.1

**Release date: June 28, 2019**

**New features:**

-   Application monitoring
    -   Plug-ins of Dubbo and MariaDB are supported.
    -   The SQL variable value bound with the PrepareStatement parameter can be captured. The setting takes effect without the need to restart the application. For more information, see [Configure advanced settings](/intl.en-US/Application monitoring/Features provided by the console/Application Settings/Custom configuration.mdsc_advanced_options).

**Optimized features:**

-   Application monitoring
    -   Dependency on Log4j is removed to avoid conflicts.

## V2.5.6

**Release date: June 7, 2019**

**New features:**

-   Application monitoring
    -   Quantile statistics is supported.

## V2.5.5

**Release date: June 3, 2019**

**New features:**

-   Application monitoring
    -   HSF-HTTP calls are supported.

## V2.5.3

**Release date: March 15, 2019**

**New features:**

-   Application monitoring
    -   The thread metrics can be reported when the application is running.
    -   The Spring Data Redis plug-in is supported.
    -   The plug-in of Druid database connection pool is supported.

## V2.5.1

**Release date: February 1, 2019**

**New features:**

-   Application monitoring
    -   Applications deployed on Container Service for Kubernetes \(ACK\) or in open source Kubernetes can be monitored. For more information, see [Install the ARMS agent for a Java application deployed in Container Service for Kubernetes](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md) and [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).
-   Browser monitoring
    -   DingTalk, Alipay, WeChat, and other mini programs can be monitored. For more information, see [Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md), [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md), [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md), and [Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor other mini programs.md).

## V2.5.0

**Release date: January 21, 2019**

**New features:**

-   Application monitoring
    -   Applications can be classified by tag.

**Optimized features:**

-   Browser monitoring
    -   The alerting feature is optimized.

## V2.4.8

**Release date: January 6, 2019**

**New features:**

-   Application monitoring
    -   Conflict detection is supported.
    -   URL convergence rules can be dynamically enabled or disabled.

## V2.4.7

**Release date: December 13, 2018**

**New features:**

-   Application monitoring
    -   Monitoring of Java applications can be enabled by using scripts in one step. For more information, see [Install the ARMS agent for a Java application by using scripts](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application by using scripts.md).
    -   PHP applications can be monitored. For more information, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md).

**Optimized features:**

-   Application monitoring
    -   The traditional method used to enable the monitoring of Java applications is optimized. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md).
-   Browser monitoring
    -   Troubleshooting of JavaScript errors is optimized. Online JavaScript code is compressed into one line. An error cannot be identified based on the error line number reported from browser. Browser monitoring can identify the error by using source maps. For more information, see [Diagnose JS errors by using ARMS browser monitoring](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md).

## V2.4.6

**Release date: October 26, 2018**

**New features:**

-   Application monitoring
    -   Monitoring of NoSQL databases is supported.
    -   The Overview page is optimized by adding three modules: application monitoring details, browser monitoring details, and product newsletter.

## V2.4.5

**Release date: September 17, 2018**

**New features:**

-   Application monitoring
    -   The components and frameworks of MongoDB are supported.

## V2.4.4

**Release date: August 17, 2018**

**New features:**

-   Application monitoring:

    -   Thread profiling is supported. When the request of a thread times out, you can locate the time consumption of all internal stacks. For more information, see [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md).
-   Browser monitoring:

    -   Resource loading details are supported. You can locate all slowly loaded resources on the page, such as images, JS, CSS, and APIs. For more information, see [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).
-   Custom monitoring:

    -   Custom monitoring is put into commercial use.

## V2.4.3.4

**Release date: July 16, 2018**

**New features:**

-   Application monitoring:
    -   Comprehensive troubleshooting is supported. You can query the distributed trace of application monitoring by trace ID. This improves the efficiency of troubleshooting.

## V2.4.3.3

**Release date: June 16, 2018**

**Optimized features:**

-   General:
    -   API operations can be called by Resource Access Management \(RAM\) users and security authentication for API calls are optimized. For more information, see [Grant different permissions to RAM users](/intl.en-US/Access control/Grant different permissions to RAM users.md).
-   Application monitoring:
    -   The Application Monitoring page is updated. More critical information is displayed on the page.
    -   The capture and analysis of memory snapshots are optimized. This improves the capture efficiency by 50%.

## V2.4.3

**Release date: May 19, 2018**

**New features:**

-   Application monitoring:
    -   The analysis of memory snapshots is supported. This allows you to view memory allocations and locate memory leaks. For more information, see [t152243.md\#](/intl.en-US/Application monitoring/Features provided by the console/Application details/Memory snapshot.md).
    -   Custom configuration of monitoring methods is supported. This allows you to dynamically configure monitoring methods, capture exceptions, and improves monitoring granularity. The configurations immediately take effect without the need to restart the machine.
    -   The Overview page of application monitoring is added. This page helps you detect and troubleshoot errors.
    -   Trace monitoring of Message Queue \(MQ\) is supported. This helps you locate delayed messages, error messages, and accumulated messages.

## V2.4.2

**Release date: April 19, 2018**

**New features:**

-   Application monitoring:

    -   JVM monitoring is supported. This allows you to monitor important metrics of JVM, such as heap memory, non-heap memory, and number of threads. For more information, see [JVM monitoring](/intl.en-US/Application monitoring/Features provided by the console/Application details/JVM monitoring.md).
    -   Host monitoring is supported. This allows you to monitor metrics of hosts, such as CPU, memory, disks, and traffic. For more information, see [t152241.md\#](/intl.en-US/Application monitoring/Features provided by the console/Application details/Host monitoring.md).
    -   Custom configuration is supported. This allows you to modify configurations on the user interface, such as trace sampling, agent switch setting, and threshold setting. For more information, see [t152246.md\#](/intl.en-US/Application monitoring/Features provided by the console/Application Settings/Custom configuration.md).
-   Browser monitoring:

    -   The sample reporting feature is supported. This reduces reports and workloads of server by using random sample reporting. For more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

## V2.4.1

**Release date: March 22, 2018**

**New features:**

-   General:
    -   Batch import and export of alert rules are supported to simplify alert management.
    -   Application monitoring of Enterprise Distributed Application Service \(EDAS\) is put into commercial use and 50% off is provided for long-term use.
-   Application monitoring:
    -   Agents in the Online state are displayed in the agent list. This allows you to view the version and status of each agent.
-   Browser monitoring:
    -   The response time is displayed in the format of quantile values rather than average values. This allows you to view the time consumption and distribution of slow requests.
-   Application monitoring:
    -   Quantile operators are supported. This allows you to view more detailed statistics of metrics in quantile values, in addition to average, maximum, and minimum values.

## V2.4.0

**Release date: February 26, 2018**

**New features:**

-   Browser monitoring and application monitoring are put into commercial use.

## V2.3.3.1

**Release date: January 31, 2018**

**New features:**

-   Monitoring of EDAS applications can be enabled by using scripts in one step. For more information, see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Start monitoring Java applications/Enable ARMS to monitor an EDAS application.md).

## V2.3.3

**Release date: January 14, 2018**

**New features:**

-   The Overview page, documentation, and product page are updated. ARMS is designed as an Application Performance Management \(APM\) service that provides the **application monitoring**, **browser monitoring**, and **custom monitoring** features.
-   The base features of the APM service are built. The alert platform and dashboards are provided to centralize data from application, browser, and custom monitoring.
-   The China \(Hangzhou\), China \(Beijing\), China \(Shanghai\), China \(Qingdao\), and China \(Shenzhen\) regions are available.

**Optimized features:**

-   The console is optimized and used across all regions in China.
-   The Alert Query page is optimized and multi-dimensional alert query is supported.

## V2.3.1

**Release date: December 14, 2017**

**New features:**

-   Most APM features for Java applications are supported. The supported features include call topology, tracing, slow transaction reports, and slow SQL query. Spring, Redis, MySQL \(RDS\), Dubbo, and more than 10 types of Java stack frameworks are supported. You can mount a Java agent to enable ARMS to monitor applications without the need to modify the application code.

**Optimized features:**

-   The configuration procedure of data set dashboard widgets is optimized. Basic and compound metrics are displayed on the same page.
-   The wizard logic for new users is optimized. By default, the wizard for new users is enabled only for the first logon.

## V2.2.6.2

**Release date: September 23, 2017**

**New features:**

-   Heat maps are available for interactive dashboards.
-   An exception splitter is provided to cleanse data for Java exceptions.
-   The mapping module between IP addresses and physical addresses is provided for data cleansing.
-   NULL can be used as a data set filter.

**Optimized features:**

-   The alert content is optimized. The log sampling content is included in the email alerts.
-   The NGINX template is optimized. The NGINX monitoring feature is updated.

## V2.2.6

**Release date: August 31, 2017**

**New features:**

-   Browser monitoring in terms of quality and performance is released.
-   MQ data sources are supported in business transactions.

## V2.2.5

**Release date: July 26, 2017**

**New features:**

-   MQ data sources can be connected to ARMS.
-   Query for millions of data records in a data set is supported.
-   Alerts of the same type are displayed together.
-   Interactive dashboards can be shared by links. This allows external users to view the dashboards without logon.
-   Light and dark themes are provided for interactive dashboards.
-   Interactive tables are optimized. Table headers can be fixed and records can be sorted in reverse chronological order.

## V2.2.4

**Release date: June 21, 2017**

**New features:**

-   Common data sets are supported.
-   Frontend visualization components are upgraded to G2. Multiple data sets are supported in a single widget.
-   Shared links of ARMS interactive dashboards are supported.
-   On-the-fly editing of data set alerts is supported.
-   Query for millions of APIs is supported.
-   XML logs can be split with line breaks in data cleansing.

## V2.2.3

**Release date: March 30, 2017**

**New features:**

-   POP APIs of data set are supported in Python.
-   The widgets of interactive dashboards are improved. The stacking mode is available for area charts.
-   The China \(Beijing\) region is available.

**Optimized features:**

-   The alerting feature is optimized. The time range, severity, and notification method of each alert can be specified based on your business requirements.
-   Dimension tables are associated with the output of API query results.

## V2.2.2

**Release date: March 8, 2017**

**New features:**

-   Dimension tables are supported. You can customize the mapping of attributes. For example, you can map a ZIP code to a specific district, city, or province.
-   The standard template for monitoring tasks is released. This allows you to create a custom monitoring task based on the template.
-   Recovery alerts are supported. When an alert is recovered, a recovery notification is sent by using an email.

**Optimized features:**

-   Interactive dashboards are optimized. Top N filtering, zero filling, and more time granularities are supported.

## V2.2.1

**Release date: February 17, 2017**

**New features:**

-   More rate operators are supported. Rate operators are suitable for multiple scenarios such as rate change analysis.
-   RAM authorization rules are supported.

**Optimized features:**

-   The response time for real-time computing of ARMS is reduced. In some cases, the response time is reduced from more than 10 seconds to less than 5 seconds.
-   Interactive dashboards are optimized. Finer granularity is available for windows zooming.

## V2.2.0

**Release date: January 23, 2017**

**New features:**

-   Interactive dashboards are released.
-   Duplication, import, and export of monitoring tasks are supported. This allows you to use the existing monitoring plans.
-   The self-check feature of monitoring tasks is supported. The self-check feature includes error statistics and error sampling.
-   Compound operators are supported.

## V2.1.0

**Release date: October 8, 2016**

**New features:**

-   Log Service LogHub, SDK, and API can be used as data sources.
-   Advanced operators in common use are available for the alerting feature. You can specify the time range as the past N minutes, days, or hours, and can set the MAX, AVG, and MIN thresholds of metrics.
-   The advanced operators named Count Distinct and Sample are supported.
-   Interactive query of data set is supported in the console.

## V2.0.0

**Release date: August 4, 2016**

**New features:**

-   ECS data sources can be connected to ARMS.
-   Multiple types of data cleansing are supported. Supported types include single, multiple, and sequential separators, KV cleansing, JSON cleansing, and custom data cleansing based on other logic, such as exception stack.
-   Multiple types of aggregation calculations are supported. Supported types include all common aggregation calculations at various time granularities, such as SUM, COUNT, and MAX.
-   Multiple types of definitions are supported for alert settings. Supported definitions include various types of content metrics, ranking, and notification methods.
-   Comprehensive solutions based on time series and other dimensions for chart customization are supported. Column charts, line charts, pie charts, flap displays, tables, and other common presentation formats and dashboard configurations are integrated. Data drilling up and down are supported.
-   Custom dashboards are supported. You can drag and drop existing alerts and charts to create a custom dashboard.

