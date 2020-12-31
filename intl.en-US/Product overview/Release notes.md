# Release notes

This topic provides the release notes of Application Real-Time Monitoring Service \(ARMS\) and describes feature changes in each release.

## V2.7.8

**Release date: November 8, 2020**

**New features:**

-   Service level objective \(SLO\) monitoring
    -   The SLO monitoring is supported for applications.

## V2.7.7.1

**Release date: November 3, 2020**

**New features:**

-   Synthetic monitoring
    -   The recorder V0.1 for synthetic monitoring is added.
    -   The synthetic monitoring scripts can be recorded if the Google Chrome browser is used.

## V2.7.7

**Release date: October 15, 2020**

**New features:**

-   Synthetic monitoring
    -   Synthetic monitoring V0.1 is added.
    -   Scheduled synthetic monitoring is supported for HTTP or HTTPS and networks in multiple cities and for multiple carriers.

## V2.7.6.2

**Release date: September 15, 2020**

**New features:**

-   Dashboards and alerting
    -   Dynamic baselines are supported for the thresholds of alerting metrics.

## V2.7.5.3

**Release date: August 20, 2020**

**New features:**

-   Application monitoring
    -   Node.js applications can be monitored.

## V2.7.4.1

**Release date: August 3, 2020**

**New features:**

-   Application monitoring
    -   AIOps automatic diagnostics supports evaluating business impacts.

## V2.7.3

**Release date: July 9, 2020**

**New features:**

-   Prometheus Monitoring
    -   By default, Function Compute can be monitored.

## V2.7.2

**Release date: June 5, 2020**

**New features:**

-   Prometheus Monitoring
    -   User-created Kubernetes clusters can be monitored.

## V2.7.1

**Release date: May 15, 2020**

**New features:**

-   Prometheus Monitoring
    -   Internal networks can be monitored and inspected based on the blackbox.

## V2.7.0

**Release date: April 2, 2020**

**New features:**

-   Application monitoring
    -   The performance issues of traces can be automatically analyzed.

## V2.6.5

**Release date: March 5, 2020**

**New features:**

-   Browser monitoring
    -   Multi-dimensional queries of performance metrics are supported.

## V2.6.2

**Release date: February 14, 2020**

**New features:**

-   Application monitoring
    -   Business monitoring is supported.
    -   The components of Spring Cloud are supported, such as WebFlux and Gateway.

## V2.6.1

**Release date: February 11, 2020**

**New features:**

-   Application monitoring
    -   Relevant features, such as obtaining metadata of microservices, are supported.

## V2.6.0.2

**Release date: January 2, 2020**

**New features:**

-   Application monitoring
    -   A new version of exception analysis is supported.

**Optimized features:**

-   Application monitoring
    -   Bugs of the Thrift plug-in are fixed.

## V2.6.0

**Release date: December 17, 2019**

**New features:**

-   Application monitoring
    -   Asynchronous traces are supported.
    -   The parameters that are called by Dubbo or HSFProvider can be recorded.

## V2.5.9.5

**Release date: November 28, 2019**

**New features:**

-   Application monitoring
    -   The jfinal-undertow plug-in is supported.

**Optimized features:**

-   Application monitoring
    -   Several bugs are fixed, including the bug of failing to obtain the thread profiling data of Dubbo.

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
    -   The logic that is used to obtain the IP addresses of network interface controllers is modified.

## V2.5.8

**Release date: August 2, 2019**

**New features:**

-   Application monitoring
    -   The dual-state alerting feature is supported. This allows you to configure alert rules for metrics that have only two states: yes and no or being and not being.
    -   The plug-ins of Dameng Database, a Chinese company, are supported.

## V2.5.7.2

**Release date: July 30, 2019**

**New features:**

-   Application monitoring
    -   Metrics of Java Virtual Machine \(JVM\) Metaspace are supported.
    -   HTTP status codes to be ignored can be customized. By default, HTTP status codes greater than 400 are counted as errors. You can customize HTTP status codes that are greater than 400 but not counted as errors. For more information, see [Configure advanced settings](/intl.en-US/Application monitoring/Console functions/Application Settings/Custom configuration.mdsc_advanced_options).

## V2.5.7

**Release date: July 11, 2019**

**Optimized features:**

-   Application monitoring
    -   The Fastjson version that is being dependent on and has security vulnerabilities is upgraded.

## V2.5.6.1

**Release date: June 28, 2019**

**New features:**

-   Application monitoring
    -   The Dubbo and MariaDB plug-ins are supported.
    -   Custom configurations allow you to obtain the value that is bound by SQL. The variable value that is bound to the PrepareStatement parameter can be captured. The setting takes effect without the need to restart the application. For more information, see [Configure advanced settings](/intl.en-US/Application monitoring/Console functions/Application Settings/Custom configuration.mdsc_advanced_options).

**Optimized features:**

-   Application monitoring
    -   Dependency on Log4j is removed to avoid conflicts.

## V2.5.6

**Release date: June 7, 2019**

**New features:**

-   Application monitoring
    -   Quantile statistics are supported.

## V2.5.5

**Release date: June 3, 2019**

**New features:**

-   Application monitoring
    -   HSF-HTTP calls are supported.

## V2.5.3

**Release date: March 15, 2019**

**New features:**

-   Application monitoring
    -   Thread metrics can be reported when applications are running.
    -   The Spring-Data-Redis plug-in is supported.
    -   The plug-in of the Druid database connection pool is supported.

## V2.5.1

**Release date: February 1, 2019**

**New features:**

-   Application monitoring
    -   Applications that are deployed on Container Service for Kubernetes \(ACK\) are supported. Application monitoring can be enabled in the console or open source environments for the applications that are deployed on ACK. For more information, see [Install the ARMS agent for a Java application deployed in Container Service for Kubernetes](/intl.en-US/Application monitoring/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md) and [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Monitor Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).
-   Browser monitoring
    -   Mini programs can be monitored. Browser monitoring can be enabled for the mini programs on DingTalk, Alipay, and WeChat, and other types of mini programs. For more information, see [Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor DingTalk mini programs.md), [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor Alipay mini programs.md), [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor WeChat mini programs.md), and [Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor other mini programs.md).

## V2.5.0

**Release date: January 21, 2019**

**New features:**

-   Application monitoring
    -   The tagging feature is added. Application sits can be classified by tag in the list of monitored applications.

**Optimized features:**

-   Browser monitoring
    -   The alerting feature is optimized.

## V2.4.8

**Release date: January 6, 2019**

**New features:**

-   Application monitoring
    -   The class conflict detection feature is added.
    -   URL convergence rules can be dynamically enabled and disabled.

## V2.4.7

**Release date: December 13, 2018**

**New features:**

-   Application monitoring
    -   Application monitoring can be enabled within a few clicks for Java applications. For more information, see [Install the ARMS agent for a Java application by using scripts](/intl.en-US/Application monitoring/Monitor Java applications/Install the ARMS agent for a Java application by using scripts.md).
    -   Application monitoring can be enabled for PHP applications. For more information, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md).

**Optimized features:**

-   Application monitoring
    -   The traditional method to enable application monitoring for Java applications is optimized. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Monitor Java applications/Manually install the ARMS agent for a Java application.md).
-   Browser monitoring
    -   The feature of locating JavaScript errors is optimized. In most cases, online JavaScript code is compressed into one line. An error cannot be located based on the error line number that is reported by the browser. Browser monitoring of ARMS can locate errors by using Source Map. For more information, see [Diagnose JS errors by using ARMS browser monitoring](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md).

## V2.4.6

**Release date: October 26, 2018**

**New features:**

-   Application monitoring
    -   Monitoring can be enabled for NoSQL databases.
    -   Brand-new Overview page: The page layout is optimized by adding the application monitoring details, browser monitoring details, and product newsletter modules.

## V2.4.5

**Release date: September 17, 2018**

**New features:**

-   Application monitoring
    -   MongoDB is supported. The supported components and frameworks include MongoDB.

## V2.4.4

**Release date: August 17, 2018**

**New features:**

-   Application monitoring:

    -   Thread profiling is supported. For threads whose requests time out, you can quickly identify the time consumption of all the internal stacks in the threads. For more information, see [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md).
-   Browser monitoring:

    -   Resource loading details are supported. You can locate all the slowly loaded resources on the page, such as images, JavaScript, CSS, and APIs. For more information, see [Slow session tracing](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).
-   Custom monitoring:

    -   Custom monitoring is put into commercial use.

## V2.4.3.4

**Release date: July 16, 2018**

**New features:**

-   Application monitoring:
    -   Comprehensive troubleshooting is supported. You can query the distributed traces of application monitoring by business ID. This makes problem diagnostics much more efficient.

## V2.4.3.3

**Release date: June 16, 2018**

**Optimized features:**

-   General:
    -   Resource Access Management \(RAM\) users can call OpenAPI. Security authentication for API calls is further improved. For more information, see [Grant different permissions to RAM users](/intl.en-US/Access control/Grant different permissions to RAM users.md).
-   Application monitoring:
    -   A brand-new revision of the Application Monitoring homepage is provided. The homepage displays more critical summary information.
    -   The feature of capturing and analyzing memory snapshots is optimized in different network environments. This improves the capture efficiency by more than 50%.

## V2.4.3

**Release date: May 19, 2018**

**New features:**

-   Application monitoring:
    -   The feature of analyzing memory snapshots is added. This provides an uninterrupted view of the distribution of memory objects and helps you quickly locate memory leaks. For more information, see [t152243.md\#](/intl.en-US/Application monitoring/Console functions/Application details/Memory snapshot.md).
    -   The feature of custom configuration of monitoring methods is added. This allows you to dynamically configure specific methods to monitor and capture exceptions, and enables more fine-grained monitoring. The configurations immediately take effect without the need to restart the machine.
    -   The Overview page of application monitoring is added. This makes issue troubleshooting and location more convenient and exact.
    -   Trace monitoring of Message Queue \(MQ\) is supported. This helps you quickly locate delayed messages, error messages, and stacked messages.

## V2.4.2

**Release date: April 19, 2018**

**New features:**

-   Application monitoring:

    -   The JVM monitoring feature is added. This allows you to monitor important metrics of JVM, such as heap memory, non-heap memory, and the number of threads. For more information, see [JVM monitoring](/intl.en-US/Application monitoring/Console functions/Application details/JVM monitoring.md).
    -   The host monitoring feature is added. This allows you to monitor a series of host performance metrics, such as CPU, memory, disks, and network traffic. For more information, see [t152241.md\#](/intl.en-US/Application monitoring/Console functions/Application details/Host monitoring.md).
    -   The custom configuration feature is added. This allows you to modify configurations on the user interface, such as trace sampling, agent switch, and threshold settings. For more information, see [t152246.md\#](/intl.en-US/Application monitoring/Console functions/Application Settings/Custom configuration.md).
-   Browser monitoring:

    -   The sample reporting configuration is supported. You can use random sample reporting to reduce reports from users and workloads. For more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

## V2.4.1

**Release date: March 22, 2018**

**New features:**

-   General:
    -   Alert rules can be imported and exported in batches. This makes alert management more convenient.
    -   Application monitoring for Enterprise Distributed Application Service \(EDAS\) is put into commercial use, and 50% off is available for long-term use.
-   Application monitoring:
    -   A list of online Agents can be viewed. The versions and status of the Agents that are installed by a user are clear at a glance.
-   Browser monitoring:
    -   The response time can be viewed in the form of quantile values rather than average values. This helps you view the time consumption and distribution of slow requests more clearly.
-   Application monitoring:
    -   Quantile operators are supported. You can view more detailed metric statistics in quantile values, in addition to average, maximum, and minimum values.

## V2.4.0

**Release date: February 26, 2018**

**New features:**

-   The browser monitoring and application monitoring features of ARMS are put into commercial use.

## V2.3.3.1

**Release date: January 31, 2018**

**New features:**

-   Application monitoring of ARMS fully supports EDAS applications. EDAS users can connect EDAS applications to ARMS applications within a few clicks. For more information, see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Monitor Java applications/Enable ARMS to monitor an EDAS application.md).

## V2.3.3

**Release date: January 14, 2018**

**New features:**

-   A brand-new homepage and documentation are provided. Major revisions are made for the product page. The product is officially positioned as a combined Application Performance Management \(APM\) product that is oriented to **application monitoring**, **browser monitoring**, and **custom monitoring**.
-   The base features that are specific to APM are basically reconstructed. This provides users with a unified alert platform and a unified interactive dashboard. The alert platform and the interactive dashboard are oriented to three subproducts: application monitoring, browser monitoring, and custom monitoring.
-   Five regions are fully supported: China \(Hangzhou\), China \(Beijing\), China \(Shanghai\), China \(Qingdao\), and China \(Shenzhen\). The China \(Shanghai\), China \(Qingdao\), and China \(Shenzhen\) regions are newly supported.

**Optimized features:**

-   The console is centralized. A centralized console is used across all the regions in China.
-   The Alert Query interface is optimized. Multi-dimensional alert queries are provided.

## V2.3.1

**Release date: December 14, 2017**

**New features:**

-   The application monitoring feature supports most general APM features of Java application monitoring, such as call topology, link tracing, slow transaction reports, and slow SQL queries. More than 10 types of Java stack frameworks that are required by standard users on the cloud are supported, such as Spring, Redis, MySQL\(RDS\), and Dubbo. You can connect to applications by mounting javaagent and do not need to modify application code.

**Optimized features:**

-   The method to configure datasets for dashboard widgets is optimized. A mixture of basic and compound indicators are displayed.
-   The prompt logic for new users is optimized. By default, the prompt for new users appears only for the first logon.

## V2.2.6.2

**Release date: September 23, 2017**

**New features:**

-   Interactive dashboards support heat maps.
-   An exception splitter is added, and supports data cleansing for Java Exception.
-   A functional module is added for mappings between IP addresses and physical addresses in the process of data cleansing.
-   The NULL type can be used as a filter condition of datasets.

**Optimized features:**

-   Alert content is optimized. The alert content in emails includes log sampling content.
-   The NGINX template is optimized. The NGINX monitoring feature that is more straightforward and easier to use is released.

## V2.2.6

**Release date: August 31, 2017**

**New features:**

-   The browser monitoring feature that is specific to quality and performance monitoring is released.
-   MQ data sources can be used for business monitoring.

## V2.2.5

**Release date: July 26, 2017**

**New features:**

-   MQ data sources can be connected to ARMS data sources.
-   Queries of millions of data records in a dataset are supported.
-   Alerts of the same type can be displayed in an aggregated way. This improves the display effect.
-   The share links of interactive dashboards can be created and connected to. This allows users to view the dashboards without logon.
-   Light and dark themes are added to interactive dashboards. This makes the interactive dashboards more aesthetic.
-   Interactive table properties are optimized. When you browse a table, you can pin the table header, and sort data in reverse chronological order.

## V2.2.4

**Release date: June 21, 2017**

**New features:**

-   General datasets are supported.
-   Frontend visualization components are fully revised and changed to G2. A single widget supports multiple datasets.
-   External links of ARMS interactive dashboards are supported.
-   On-the-fly editing of dataset alerts is supported.
-   The API supports queries of millions of data records.
-   XML logs can be split by line breaks in data cleansing.

## V2.2.3

**Release date: March 30, 2017**

**New features:**

-   The Pop API of datasets is supported in Python.
-   The widgets of interactive dashboards are improved. The stacking mode is available for area charts.
-   The China \(Beijing\) region is available.

**Optimized features:**

-   The alerting feature is overall optimized. The time to take effect, the alert severity, and the alerting method can be flexibly specified for a single alert.
-   API query results can be associated with dimension tables for output.

## V2.2.2

**Release date: March 8, 2017**

**New features:**

-   The dimension table feature is supported. This allows you to customize the mapping relationships of attributes. For example, you can map the ZIP code of a city to the province, city, and district of a specific city.
-   A standard task template is released. This allows you to quickly customize monitoring tasks based on the standard task template.
-   The alert recovery feature is added. When an alert is recovered, a notification is sent by email.

**Optimized features:**

-   Interactive dashboards continue to be optimized. TopN filtering and zero filling are added, and more time granularities are supported.

## V2.2.1

**Release date: February 17, 2017**

**New features:**

-   More rate operators are supported. Rate operators apply to scenarios, such as statistics of rate changes.
-   RAM authorization rules are supported.

**Optimized features:**

-   Response time for real-time computing of ARMS is significantly reduced. In some scenarios, response time is shortened from more than 10 seconds to less than 5 seconds.
-   Interactive dashboards continue to be optimized. Finer granularity is supported for the zooming modes of various windows.

## V2.2.0

**Release date: January 23, 2017**

**New features:**

-   Interactive dashboards are released.
-   Tasks can be copied, imported, and exported. This helps you quickly copy existing monitoring plans.
-   Self-check is supported for tasks of users, including error statistics and error sampling.
-   Compound operators are supported.

## V2.1.0

**Release date: October 8, 2016**

**New features:**

-   Log Service LogHub, SDKs, and APIs can be used as data sources.
-   The alerting feature supports various general advanced operators. You can specify the past N minutes, days, and hours, and can set the MAX, AVG, and MIN thresholds of metrics.
-   The advanced operators Count Distinct and Sample are supported.
-   An interactive search interface is supported for datasets.

## V2.0.0

**Release date: August 4, 2016**

**New features:**

-   The Elastic Compute Service \(ECS\) data that is collected in the form of logs can be connected.
-   Various types of cleansing and computing are supported: single, multiple, and sequential delimiters, KV cleansing, JSON cleansing, and cleansing based on other various custom logic, such as exception stacks.
-   Multiple types of aggregation calculations are supported: all the general aggregation calculations based on various time granularities, such as SUM, COUNT, and MAX.
-   Business alerting settings support the definitions of various content metrics, severity differentiation, and various notification delivery methods for contacts.
-   A set of solutions based on time series or other similar dimensions are provided for you to customize display charts. General display forms, such as column charts, line charts, pie charts, ticker boards, and tables, and dashboard configurations are integrated. Data drilling up and down are supported.
-   The defined alerts and charts can be dragged and dropped to customize dashboards.

