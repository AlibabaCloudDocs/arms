# View the analysis results of SQL performance

On the Database Calls page, you can view the number of SQL calls, the average time consumption, and related traces for each SQL statement. This helps you locate SQL performance issues.

## View SQL analysis results

To view SQL statistics and analysis results, perform the following steps.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click **Applications**. At the top of the Applications page, select a region as required. Then, click the name of the application that you want to check.

3.  In the left-side navigation pane, click **Database Calls**. On the **SQL Analysis** tab, view the following metrics:

    -   The number of times SQL statements are called per minute and the chart of the average response time for the calls within the specified period of time
    -   The number of times a specific SQL statement is called and the average response time for the calls within the specified period of time
4.  On the **SQL Analysis** tab, perform the following steps as required:

    -   Click **Call Statistics** in the **Actions** column. The number of times the SQL statement is called per minute and the chart of the average response time for the calls within the specified period of time are displayed.
    -   Click **Trace Query** in the **Actions** column. All the traces that are related to the SQL statement are displayed on the **Traces** tab.

**Note:** To switch to another application in the same region, click the application name drop-down list in the upper-left corner and select another application.

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is `YYYY-MM-DD`, The time format is `HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

[Overview](/intl.en-US/Before you begin/Overview.md)

[Manage applications and tags](/intl.en-US/Operations in the Console/Application management/Manage applications and tags.md)

