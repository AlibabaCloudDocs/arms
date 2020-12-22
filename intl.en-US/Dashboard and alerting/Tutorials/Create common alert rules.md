# Create common alert rules

Application Real-Time Monitoring Service \(ARMS\) provides multiple alert rule configuration templates for typical scenarios, such as application monitoring alert scenarios and browser monitoring alert scenarios. You can use the templates to create frequently used alert rules.

ARMS comes with the following alert templates:

-   Application monitoring
    -   DefaultAPM-DB-Alert: This template is used to generate alerts for long database response time and database call errors.
    -   DefaultAPM-Exception-Alert: This template is used to generate alerts for call timeout and call errors.
    -   DefaultAPM-Host-Alert: This template is used to generate alerts for high CPU usage and insufficient disk space.
    -   DefaultAPM-Process-Alert: This template is used to generate alerts for process status.
    -   DefaultAPM-GC-Alert: This template is used to generate alerts for excessive full garbage collection \(GC\) events, long full GC duration, and long young GC duration.
-   Browser monitoring
    -   DefaultRetcodeAlert: This template is used to generate alerts for a high JavaScript \(JS\) error rate and excessive JS errors.

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Template Management** to go to the Alert Template Management page.


## Create alert rules for application monitoring by using the DefaultAPM-DB-Alert template

To create an alert rule for determining whether database exceptions occur, find the **DefaultAPM-DB-Alert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses two metrics as alert triggers. An alert event is generated when one of the following criteria is met:

-   Long database response time: The response time of the call to the application database is greater than or equal to 2 seconds per minute on average within 5 minutes. Set Type to **Database\_Metric** and the metric to **DB\_RT\_ms**. The rule is that the average response time in the last 5 minutes is greater than or equal to 2000.
-   Database call error: The average number of errors that occur when the application calls a database is greater than or equal to once per minute during 5 minutes. Set Type to **Database\_Metric** and the metric to **DB\_ErrorCount**. The rule is that the average number of errors in the last 5 minutes is greater than or equal to 1.

## Create alert rules for application monitoring by using the DefaultAPM-Exception-Alert template

To create an alert rule for determining whether application call exceptions occur, find the **DefaultAPM-Exception-Alert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses two metrics as alert triggers. An alert event is generated when one of the following criteria is met:

-   Call timeout: The average time of inbound API calls of the application is greater than or equal to 2 seconds per minute during 5 minutes. Set Type to **Invocation\_Statistic** and the metric to **Invocation\_RT\_ms**. The rule is that the average time in the last 5 minutes is greater than or equal to 2000.
-   Call error: The number of errors that occur during inbound API calls of the application is greater than or equal to once per minute during 5 minutes. Set Type to **Invocation\_Statistic**, and the metric to **Invocation\_ErrorCount**. The rule is that the average number of call errors in the last 5 minutes is greater than or equal to 1.

## Create alert rules for application monitoring by using the DefaultAPM-Host-Alert template

To create an alert rule for determining whether any exceptions occur to the node on which an application is installed, find the **DefaultAPM-Host-Alert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses two metrics as alert triggers. An alert event is generated when one of the following criteria is met:

-   High CPU usage: The CPU usage of the node on which the application is installed is greater than or equal to 90% per minute during 5 minutes. Set Type to **Host\_Monitoring**, and the metric to **Node\_User\_CPU\_percent**. The rule is that the average value in the last 5 minutes is greater than or equal to 90.
-   Insufficient disk space: The average free disk space of the node on which the application is installed is less than or equal to 1 MB per minute during 5 minutes. Set Type to **Host\_Monitoring**, and the metric to **Node\_Disk\_Free\_byte**. The rule is that the average free disk space in the last 5 minutes is less than or equal to 1048576, that is, 1 MB.

## Create alert rules for application monitoring by using the DefaultAPM-Process-Alert template

To create an alert rule for determining whether process exceptions occur, find the **DefaultAPM-Process-Alert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses one metric as the alert trigger. An alert event is generated when the following criteria is met:

-   Process status: A process exception occurs. Set Type to **JVM\_Monitoring**, and the metric to **JVM\_ThreadCount**. The rule is that the average value in the last 1 minute drops by more than 50% from the previous hour.

## Create alert rules for application monitoring by using the DefaultAPM-GC-Alert template

To create an alert rule for determining whether garbage collection \(GC\) exceptions occur, find the **DefaultAPM-GC-Alert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses three metrics as alert triggers. An alert event is generated when all the following three criteria are met:

-   Excessive full GC events: The average number of full GC events is greater than or equal to twice per minute during 10 minutes. Set Type to **JVM\_Monitoring** and the metric to **JVM\_FullGC\_Count**. The rule is that the average value in the last 10 minutes is greater than or equal to 2.
-   Excessive full GC time consumption: The average time required for full GC events is greater than or equal to 10 seconds per minute during 10 minutes. Set Type to **JVM\_Monitoring** and the metric to **JVM\_FullGC\_Time\_ms**. The rule is that the average value in the last 10 minutes is greater than or equal to 10000, that is, 10 seconds.
-   Excessive young GC time consumption: The total time required by young GC events of the application is greater than or equal to 5 seconds during 1 minutes. Set Type to **JVM\_Monitoring** and the metric to **JVM\_YoungGC\_RT\_ms**. The rule is that the total time in the last 1 minute is greater than or equal to 5000, that is, 5 seconds. You can modify the threshold as needed.

## Create alert rules for browser monitoring by using the JS exception alert template

To create an alert rule for determining whether JavaScript \(JS\) exceptions occur, find the **DefaultRetcodeAlert** template and click **Create Alert** in the **Actions** column.

As shown in the preceding figure, this alert rule uses two metrics as alert triggers. An alert event is generated when the following two criteria are met:

-   High JS error rate: The average JS error rate of the frontend application is greater than or equal to 20% during 10 minutes. Set Type to **Page\_Metric** and the metric to **JS\_Error\_Rate**. The rule is that the average JS error rate in the last 10 minutes is greater than or equal to 0.2, that is, 20%.
-   Excessive JS errors: The total number of JS errors of the frontend application is greater than or equal to 20 during 10 minutes. Set Type to **Page\_Metric** and the metric to **JS\_Error\_Count**. The rule is that the total number of JS errors during the last 10 minutes is greater than or equal to 20.

## References

For more information about the fields in alert rules and **advanced configuration**, see [Description of basic fields](/intl.en-US/Dashboard and alerting/Create an alert.md).

