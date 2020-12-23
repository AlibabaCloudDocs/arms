# View SQL performance analysis

The database call page displays the call times, average time consumption, and call links of each SQL statement to help you locate SQL performance problems.

## View SQL analysis

Follow these steps to view the SQL statistics and analysis of the application.

1.  Log on [Tracing Analysis console](https://tracing-sg.console.aliyun.com/).

2.  In the left-side navigation pane, click**Application List**, And inApplication ListSelect a region and click the application name.

3.  In the left-side navigation pane, click**Database call**, And then choose**SQL analysis**On the Tab Page, view the following metrics:

    -   Displays the number of SQL calls per minute and average elapsed time within a specified period.
    -   The number of times an SQL statement is called and the average time consumed during the selected period.
4.  In**SQL analysis**On the Tab Page, perform the following operations as needed:

    -   In**Operation**Column, click**Call statistics**To view the chart of the number of calls per minute and the average time consumed by a specific SQL statement within the selected time range.
    -   In**Operation**Column, click**Link query**In the**Call link**Tab page to view all call links related to the corresponding SQL statement.

**Note:** To switch to another application in the same region, click the application name drop-down list in the upper-left corner and select another application.

## Set the query time range

You can select a preset time range or enter a custom time range.

-   Click the time option in the upper-right corner of the page, and then click a preset time range, such as **Last 30 minutes**,**This week**,**Last 30 days**.
-   If no preset time range meets your requirements, click **Custom**. Select the start time and end time from the calendar, or enter them manually in the text box. Then, click **OK**.

    **Note:** The date format is`YYYY-MM-DD`, The time format is`HH:MM`.


![Time Picker](../images/p53830.png "Query time range selector")

[Before you begin](/intl.en-US/Preparations/Before you begin.md)

[Manage apps and tags](/intl.en-US/Console guide/Application management/Manage applications and tags.md)

