# Browser monitoring dashboard

Application Real-Time Monitoring Service \(ARMS\) provides the dashboard of the browser monitoring feature. This allows you to view all the critical monitoring data of the monitored application in real time.

## Procedure

1.  Log on to the [ARMS console](https://arms.console.aliyun.com/#/home). In the left-side navigation pane, click **Browser Monitoring**.
2.  On the **Browser Monitoring** page, click the name of the application.
3.  On the Overview page, click **Dashboard** in the upper-right corner.
4.  On the Dashboard page, you can view the browser monitoring data of the application. The monitoring data includes the JavaScript \(JS\) error rate and API request success rate.

## Features

The dashboard of ARMS browser monitoring provides all the critical monitoring data of the monitored application in real time. We recommend that you display the dashboard on a big screen.

**Note:** The monitoring data can be updated once a minute.

## Related operations

-   View the monitoring data on the dashboard.
-   Move the pointer over the curve in a chart. The statistics at the point in time appears.
-   To show the dashboard in full screen, click **Full Screen** in the upper-right corner.

## Parameters

The dashboard of ARMS browser monitoring includes the following parameters.

-   JS error rate
    -   JS Error Rate: the JS error rate.
    -   Compared with Yesterday's Average: the increase or decrease ratio of the average JS error rate compared with the average JS error rate in the previous day.
    -   Statistical Chart: the curve of the JS error rate in the last hour.
    -   Page Ranked by Error Rate: the JS error rate ranking.
-   Alerts in the last 24 hours
    -   Alarms: the number of alerts.
    -   Recent 3 Alarms: the alerts from browser monitoring in the last 24 hours.
-   PV/UV
    -   Today's PV: the number of page views \(PVs\) of the monitored application on the current day.
    -   Today's UV: the number of unique visitors \(UVs\) of the monitored application on the current day.
    -   Compared with Yesterday: the increase or decrease ratio of PVs and UVs compared with the PVs and UVs in the previous day.
    -   Statistical Chart: the curve of PVs or UVs in the last hour.
    -   Statistical Table: the top five regions with the most PVs and UVs and their corresponding PVs and UVs.
    -   High Page View TOP5: the top five services with the most PVs.
-   API request success rate
    -   API Request Success Rate: the success rate of API requests.
    -   Compared with Yesterday's Average: the increase or decrease ratio of the API request success rate compared with the API request success rate in the previous day.
    -   Statistical Chart: the curve of the API request success rate in the last hour.
    -   Service Ranked by API Success Rate: the API request success rate ranking.
-   Page speed
    -   Page Speed: the First Paint Time \(FPT\). Unit: milliseconds.
    -   Compared with Yesterday's Average: the increase or decrease ratio of the page speed compared with the average page speed in the previous day.
    -   Statistical Chart: the curve of the page speed in the last hour.
    -   Low Page Speed Top 5: the top five services with the lowest page speeds.

**Related topics**  


[Page speed](/intl.en-US/Browser monitoring/Console functions/Page speed.md)

[JS error diagnosis](/intl.en-US/Browser monitoring/Console functions/JS error diagnosis.md)

[API request](/intl.en-US/Browser monitoring/Console functions/API request monitoring.md)

[Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

