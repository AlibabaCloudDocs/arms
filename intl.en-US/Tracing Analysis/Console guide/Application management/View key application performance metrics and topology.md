# View key application performance metrics and topology

The application overview page displays the key performance metrics and topology of your application.

After the application data is reported to Tracing Analysis, Tracing Analysis monitors your application. On the Application Overview page, you can quickly view key metrics for application performance and view the upstream and downstream dependencies of an application using the topology.

## View key application performance metrics

You can view the key metrics of application performance on the Overview analysis tab.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **application list**. On the top of the application list page, select a region, and then click the application name.

3.  On the Application Overview page, view the following key metrics on the Overview analysis tab.

    -   The total number of requests, average response time, number of abnormal calls, and Span in the selected time range, and how these indicators change from the previous week to the previous day or previous week.
    -   The line chart of how many times your application is called by upstream components and the response time, and how many times your application calls downstream services and the response time.
    -   The top 10 APIs with the lowest call speed and their average response time sequence curves.
    ![General Overview Tab](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/pg_app_overview_tab_general.png "Overview analysis")


## View the application topology

On the topology tab, you can have a better view of the upstream and downstream components of your application and their call relations, allowing you to quickly identify the performance bottlenecks of your application.

1.  In the left-side navigation pane, click **application list**. On the top of the application list page, select a region, and then click the application name.

2.  On the Application Overview page, click the **Topology Graph** tab. On the Topology Graph tab, you can view the following information:

    -   The call topology of the application within the selected time range.
    -   The number of calls, average response time, and error rate of the client, provider, and internal calls within the selected time.
    -   The sequence time chart of the number of requests, response time, and error rate per minute within the specified period.

![Topology Tab](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/pg_app_overview_tab_topo.png "Topology tab")

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is`YYYY-MM-DD`, The time format is`HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

**Related topics**  


[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

