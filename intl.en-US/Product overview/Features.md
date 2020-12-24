# Features

Application Real-Time Monitoring Service \(ARMS\) provides a series of custom monitoring features. These features include data import, computing, storage, visualization, and alerting. ARMS can call and be called by APIs of downstream services.

The following figure shows the ARMS features.

![ARMS Features](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9260537751/p43315.png)

The following section describes these features.

-   Multi-dimensional browser monitoring

    -   High timeliness: detects the response time and error rate of accessed websites in real time.
    -   Multi-dimensional monitoring and analysis: analyzes access speeds and errors by region, carrier, and browser.
    -   Page exception monitoring: monitors and diagnoses the performance and success rate of a large number of asynchronous data calls of applications.
-   Efficient and easy-to-use application monitoring

    -   Application topology self-discovery: generates the call relationship map among distributed applications based on the dynamic analysis and intelligent computing of the remote procedure call \(RPC\) information.
    -   Drill-down metric analysis in common diagnosis scenarios: analyzes metrics such as the application response time, number of requests, and error rate. Then, this feature displays the analysis data by application, transaction, and database.
    -   Capturing of abnormal and slow transactions: analyzes timeouts and exceptions based on traces, and associates the transactions with API calls, for example, with specific SQL statements and message queues.
    -   Transaction snapshot query: collects trace-based transaction errors and identifies the sources of exceptions or errors by checking detailed data.
-   Powerful custom monitoring

    -   Rich data sources: supports various types of real-time data sources, such as logs, SDK, Message Queue \(MQ\), and LogHub.
    -   Flexible real-time computing and storage orchestration: allows you to orchestrate real-time computing and storage modes based on specified dimensions and computing modes.
    -   Flexible integration with alerts or dashboards: integrates monitoring datasets with ARMS alerts and dashboards. This way, ARMS provides monitoring capabilities for various scenarios.
    -   Reference scenario templates: provides a large number of reference scenario templates, such as NGINX monitoring, exception monitoring, and e-commerce monitoring.
-   ARMS also provides the following features:

    -   Flexible real-time computing jobs
        -   Supports drag-and-drop modular programming of real-time computing and supports most logic expressions, such as general mathematical operations, regular expressions, and if and else statements.
        -   Supports a variety of real-time computing and storage operators. These operators include SUM, COUNT, MAX, MIN, SAMPLE, TOPN, and COUNT DISTINCT.
    -   Stable and efficient time series and event storage
        -   Aggregates data online in a continuous manner to ensure a controllable data capacity.
        -   Supports intelligent hierarchical storage policies.
        -   Supports a maximum of three levels of drill-down indexes.
    -   Custom alert settings
        -   Supports alerts for moving average and maximum values within a time period.
        -   Supports custom alert content.
        -   Provides multiple alert notification methods, such as email, SMS message, and DingTalk notification.
    -   Flexible customization of interactive dashboards
        -   Provides rich presentation widgets, such as bar charts, heat maps, pie charts, and ticker boards.
        -   Supports dashboard sharing and full screen display.
    -   Flexible integration with downstream applications
        -   Supports integration with APIs of Java, Python, Perl, and C\# applications.
        -   Supports integration with other display tools such as DataV.

