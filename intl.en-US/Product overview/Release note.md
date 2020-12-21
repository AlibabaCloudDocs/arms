# Release note

This topic provides a version release record of Application Real-Time Monitoring Service \(ARMS\) to describe the feature changes of previous ARMS releases.

## V2.5.2

**Date: February 21, 2019**

**New features:**

-   Application monitoring
    -   Supported one-click monitoring of applications deployed on Elastic Compute Service \(ECS\) instances.

## V2.5.1

**Date: February 1, 2019**

**New features:**

-   Application monitoring
    -   Supported using the ARMS console to monitor applications deployed in Container Service for Kubernetes or in open-source Kubernetes environments. For more information, see [Install the ARMS agent for Java applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for Java applications in Container Service for Kubernetes.md) and [Install the ARMS agent for applications in open-source Kubernetes environments](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in open-source Kubernetes environments.md).
-   Browser monitoring
    -   Supported browser monitoring for DingTalk, Alipay, WeChat, and other mini programs. For more information, see [Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md), [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md), [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md), and [Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor other mini programs.md).

## V2.5.0

**Date: January 21, 2019**

**New features:**

-   Application monitoring
    -   Added the label function. You can classify application sites by label in the monitored application list.

**Optimization and improvement:**

-   Browser monitoring
    -   Optimized the alert function.

## V2.4.8

**Date: January 6, 2019**

**New features:**

-   Application monitoring
    -   Supported class conflict detection.
    -   Supported dynamically enabling and disabling URL convergence rules.

## V2.4.7

**Date: December 13, 2018**

**New features:**

-   Application monitoring
    -   Supported one-click monitoring of Java applications. For more information, see [Quickly install the ARMS agent for Java applications by using scripts](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for Java applications by using scripts in one click.md).
    -   Supported PHP application monitoring. For more information, see [Install the ARMS agent for common PHP applications](/intl.en-US/Application monitoring/Start monitoring PHP applications/Install the ARMS agent for common PHP applications.md).

**Optimization and improvement:**

-   Application monitoring
    -   Optimized the traditional method of enabling Java application monitoring. For more information, see [Manually install the ARMS agent for Java applications](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md).
-   Browser monitoring
    -   Optimized the JavaScript \(JS\) error locating function. Online JS code is often compressed into one line, making error locating impossible based on the browser-reported erroneous line number. ARMS browser monitoring can restore the error location through source maps. For more information, see [Use ARMS browser monitoring for JS error diagnosis](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors with ARMS browser monitoring.md).

## V2.4.6

**Date: October 26, 2018**

**New features:**

-   Application monitoring
    -   Supported NoSQL database monitoring.
    -   Provided a new overview page, with an optimized page layout and new modules, such as application monitoring details, browser monitoring details, and product express.

## V2.4.5

**Date: September 17, 2018**

**New features:**

-   Application monitoring
    -   Included MongoDB in supported components and frameworks.

## V2.4.4

**Date: August 17, 2018**

**New features:**

-   Application monitoring:

    -   Supported thread profiling. When a thread encounters request time-out, you can quickly locate the time consumption of all internal stacks. For more information, see [Use ARMS TProf to analyze code problems](/intl.en-US/Application monitoring/Tutorials/Use ARMS TProf to analyze code problems.md).
-   Browser monitoring:

    -   Supported resource loading details. You can quickly locate all slowly loaded resources on the page, such as images, JS, CSS, and APIs. For more information, see [Slow session tracking](/intl.en-US/Browser monitoring/Tutorials/Slow session tracing.md).
-   Custom monitoring:

    -   Commercially available.

## V2.4.3.4

**Date: July 16, 2018**

**New features:**

-   Application monitoring:
    -   Supported comprehensive troubleshooting. You can query the distributed trace of application monitoring through business ID, which greatly improves the problem diagnosis efficiency.

## V2.4.3.3

**Date: June 16, 2018**

**Optimization and improvement:**

-   General:
    -   Supported API calls by RAM users and improved security authentication for API calls. For more information, see [Create and authorize RAM sub-accounts](/intl.en-US/Access control/Grant different permissions to RAM users.md).
-   Application monitoring:
    -   Revised the homepage of application monitoring to show more core summaries.
    -   Optimized the memory snapshot capture and analysis function in different network environments, which improves the efficiency of capture by more than 50%.

## V2.4.3

**Date: May 19, 2018**

**New features:**

-   Application monitoring:
    -   Added the memory snapshot analysis function, allowing you to grasp the distribution of memory objects with a glance and quickly locate memory leaks. For more information, see [Memory snapshots](/intl.en-US/Application monitoring/Function specification/Application details/Memory snapshot.md).
    -   Supported the custom configuration of monitoring methods, allowing you to dynamically configure methods to monitor and capture exceptions, with an increased monitoring granularity. The configuration takes effect immediately without restarting the machine.
    -   Added the application monitoring overview page to facilitate problem locating and troubleshooting.
    -   Added Message Queue \(MQ\) trace monitoring to quickly locate message delay, errors, and message accumulation.

## V2.4.2

**Date: April 19, 2018**

**New features:**

-   Application monitoring:

    -   Added the JVM monitoring function to monitor a series of important JVM metrics, including heap memory, non-heap memory, and number of threads. For more information, see [JVM monitoring](/intl.en-US/Application monitoring/Function specification/Application details/JVM monitoring.md).
    -   Added the host monitoring function to monitor a series of host performance metrics, including the CPU, memory, disks, and network traffic. \[ [Host monitoring](/intl.en-US/Application monitoring/Function specification/Application details/Host monitoring.md).
    -   Added the custom configuration function, allowing you to modify configurations directly in the console, including trace sampling, agent switch setting, and threshold setting. For more information, see [Custom configurations](/intl.en-US/Application monitoring/Function specification/Application Settings/Custom configuration.md).
-   Browser monitoring:

    -   Added the sample reporting configuration feature, which reduces the number of user reports and loads through random sample reporting. For more information, see [Configurations of the browser monitoring SDK](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

## V2.4.1

**Date: March 22, 2018**

**New features:**

-   General:
    -   Added alert rules, which support batch import and export of alerts to make alert management more convenient.
    -   Supported monitoring of applications in Enterprise Distributed Application Service \(EDAS\), with a 50% off discount for long-term use.
-   Application monitoring:
    -   Supported display of an online agent list, allowing you to be informed of the installed agent versions and their statuses.
-   Browser monitoring:
    -   Supported display of the response time in the format of quantile rather than average values, allowing you to view the response time and distribution of slow requests more clearly.
-   Application monitoring:
    -   Supported quantile operators, allowing you to view more detailed metric statistics in the format of quantile values, in addition to average, maximum, and minimum values.

## V2.4.0

**Date: February 26, 2018**

**New features:**

-   ARMS browser monitoring and application monitoring are commercially available.

## V2.3.3.1

**Date: January 31, 2018**

**New features:**

-   Supported all EDAS applications. EDAS users can connect EDAS applications to ARMS with one click. For more information, see [Install the ARMS agent for applications in EDAS with one click](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in EDAS in one click.md).

## V2.3.3

**Date: January 14, 2018**

**New features:**

-   Provided a brand new homepage and documentation with an overhauled product page. The product is officially positioned as an APM product, integrating **application monitoring**, **browser monitoring**, and **custom monitoring**.
-   Optimized the APM-oriented base function to provide a centralized alert platform and interactive dashboard for the following modules: application monitoring, browser monitoring, and custom monitoring.
-   Supported the following regions: China \(Hangzhou\), China \(Beijing\), China \(Shanghai\) \(new\), China \(Qingdao\) \(new\), and China \(Shenzhen\) \(new\).

**Optimization and improvement:**

-   Optimized the console: one console used across all regions in China.
-   Optimized the alert query page, and supported multi-dimensional alert query.

## V2.3.1

**Date: December 14, 2017**

**New features:**

-   Supported most common Java APM functions, including call topology, tracing, slow transactions reports, and slow SQL querying. Supported more than 10 types of Java stack frameworks required by common cloud users, such as Spring, Redis, MySQL \(RDS\), and Dubbo. You can connect applications to ARMS by installing the Java agent without modifying application code.

**Optimization and improvement:**

-   Optimized the dashboard widget dataset setting. Basic and compound metrics can be displayed on the same page.
-   Optimized the new user tour guide logic. By default, the new user prompt function is enabled only upon initial logon.

## V2.2.6.2

**Date: September 23, 2017**

**New features:**

-   Supported heat map on the interactive dashboard.
-   Added the exception splitter to support data cleansing of Java exceptions.
-   Added the IP address-to-physical address mapping module to the data cleansing process.
-   Supported a value of the NULL type for a dataset filter.

**Optimization and improvement:**

-   Optimized the alert content. The email alert now contains the log sampling content.
-   Optimized the NGINX template, and provided more straightforward and easy-to-use NGINX monitoring functions.

## V2.2.6

**Date: August 31, 2017**

**New features:**

-   Released quality- and performance-focused browser monitoring.
-   Supported MQ data sources in business monitoring.

## V2.2.5

**Date: July 26, 2017**

**New features:**

-   Supported MQ data sources in ARMS.
-   Supported query of millions of data records in a dataset.
-   Displayed alerts of the same type together for a cleaner look.
-   Supported creation and access of the interactive dashboard sharing links by external users so that they can view the dashboard without logon.
-   Added the black-and-white theme to the interactive dashboard for improved aesthetic effect.
-   Enhanced interactive tables. The column header can be frozen, and records can be sorted in reverse chronological order.

## V2.2.4

**Date: June 21, 2017**

**New features:**

-   Supported common datasets.
-   Upgraded the front-end visualization component to G2, and supported multiple datasets in a single widget.
-   Supported external trace of ARMS interactive dashboards.
-   Supported on-the-fly editing of dataset alerts.
-   Supported querying of millions of data records with APIs.
-   Supported splitting of XML and logs with line breaks in data cleansing.

## V2.2.3

**Date: March 30, 2017**

**New features:**

-   Supported Python for dataset POP APIs.
-   Enhanced interactive dashboard widgets. For example, the area chart supports stacking mode.
-   Added the China \(Beijing\) region.

**Optimization and improvement:**

-   Optimized the overall alert function, and supported flexible setting of the alert time range, alert severity, and notification method for individual alerts.
-   Supported associated output of dimension tables for API query results.

## V2.2.2

**Date: March 8, 2017**

**New features:**

-   Supported dimension tables. You can customize the mapping of attributes, for example, mapping a postal code to a specific district, city, or province.
-   Released the standard job template, allowing you to quickly create a custom monitoring job based on the standard job template.
-   Added the data recovery function. When an alert is cleared, a notification will be sent by email.

**Optimization and improvement:**

-   Further optimized the interactive dashboard, and added top N filtering, zero fill, and time granularities.

## V2.2.1

**Date: February 17, 2017**

**New features:**

-   Added rate operators, applicable to scenarios such as rate change statistics.
-   Supported RAM authorization rules.

**Optimization and improvement:**

-   Reduced the response time dramatically for ARMS real-time computing. In some cases, the response time is shortened from more than 10s to less than 5s.
-   Further optimized the interactive dashboard, with finer control over resizing of various windows.

## V2.2.0

**Date: January 23, 2017**

**New features:**

-   Released the interactive dashboard function.
-   Supported duplication, import, and export of jobs, allowing you to quickly duplicate existing monitoring plans.
-   Supported user job self-check, including job error statistics and error sampling.
-   Supported compound operators.

## V2.1.0

**Date: October 8, 2016**

**New features:**

-   Added Log Service LogHub, SDK, and API data sources.
-   Supported common advanced operators in alerts. You can specify the time range as the past N minutes, days, or hours, and can set the MAX, AVG, and MIN thresholds of metrics.
-   Supported advanced operators: Count Distinct and Sample.
-   Added the interactive dataset query page.

## V2.0.0

**Date: August 4, 2016**

**New features:**

-   Supported ECS data sources.
-   Supported various cleansing calculations, including single, multiple, and sequential separators, KV cleansing, JSON cleansing, and other custom cleansing logic \(such as exception stack\).
-   Supported multiple types of aggregation calculations, including all common aggregation calculations at various time granularities, such as SUM, COUNT, and MAX.
-   Supported definition of various types of content metrics, ranking, and notification methods for alert settings.
-   Supported comprehensive solutions based on time series and other similar dimensions for chart customization, integrated with common presentation formats and dashboard configurations, such as column chart, line chart, pie chart, flap display, and table, and provided data drill up and drill down capabilities.
-   Supported creation of a dashboard by dragging and dropping existing alerts and charts.

