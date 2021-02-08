# View the key performance metrics and topology of an application

You can view the key performance metrics and topology of an application on the Application Overview page.

After the data of an application is reported to Tracing Analysis, Tracing Analysis starts to monitor the application in an all-around manner. On the Application Overview page, you can view the key performance metrics of the application. You can also view the topology to check the upstream and downstream services of your application and their dependencies.

## View the key performance metrics of an application

You can view the key performance metrics of an application on the Application Overview page.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application that you want to check.

3.  On the Overall Analysis tab of the Application Overview page, view the following key performance metrics:

    -   The total number of requests, average response time, number of errors, and number of spans in the specified time range, and the percentage changes between the statistics of the same day last week or last day and the current statistics.
    -   The line chart of how many times your application is called by upstream services and the response time, and how many times your application calls downstream services and the response time.
    -   The 10 spans that require the most time and their line charts of average response time.
    ![General Overview Tab](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/pg_app_overview_tab_general.png "Overall Analysis tab")


## View the topology of an application

On the Topology Graph tab, you can obtain a better view of the upstream and downstream services of your application and the call relationships between the services and the application. Then, you can identify the performance bottlenecks of your application.

1.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application that you want to check.

2.  On the Application Overview page, click the **Topology Graph** tab. On the Topology Graph tab, view the following information:

    -   The topology of service calls for the application in the specified time range.
    -   The numbers of calls on the client, calls on the server, and internal calls for the application, average response time, and error rate in the specified time range.
    -   The line charts of the number of requests, response time, and error rate in each minute of the specified time range.

![Topology Tab](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/xtrace/pg_app_overview_tab_topo.png "Topology Graph tab")

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is `YYYY-MM-DD`, The time format is `HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

**Related topics**  


[Overview](/intl.en-US/Before you begin/Overview.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

