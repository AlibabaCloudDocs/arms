# Create common alarm rules

By default, ARMS provides alarm rule configuration templates in multiple typical scenarios, including application monitoring alarms and frontend monitoring alarms. These templates help you quickly create common alarm rules.

By default, ARMS provides the following alarm templates:

-   Application Monitoring
    -   Default Alert of Application Monitoring-database exception alert template: Alert template for long Database response time or database call error
    -   Default Alert for application monitoring-alert template for abnormal calls: Alert template for timeout calls or incorrect calls
    -   Default application monitoring alarms-host monitoring alarm Template: alarms generated when the CPU usage is too high or the disk space is insufficient
    -   Default Alert for application monitoring-process exception alert template: Alert for process survival scenarios
    -   Default Alert template for application monitoring-GC exception alert template: an alert is triggered if there are too many full GC, full GC time-consuming, or young GC time-consuming scenarios.
-   Browser monitoring
    -   Default alarm template for browser monitoring: Alarms for scenarios with high JS error rate or excessive JS errors

## Function entry

1.  In the left-side navigation pane, choose**Alarm Management** \> **Alert Template management**, Jump toAlert Template managementPage.


## Create application monitoring-database exception alarm

If you need to create an alarm rule that determines whether the database of the application is abnormal, you can click**Default Alert of Application Monitoring-database exception alert**Right**Operation**Column**Create an alarm**.

![Db_alarm_database_exception](../images/p82385.png)

As shown in the preceding figure, the alarm rule is based on two metrics. An alarm event is generated when one of the conditions is met.

-   Too long Database response time: the average response time of an application&\#39;s database call within 5 minutes exceeds or is equal to 2 s per minute. The corresponding alarm metric type is**Database metrics**The alarm indicator is**Database call response time \_ MS**The rule is that the average value in the last five minutes is greater than or equal to 2000.
-   Database call errors: the number of application database call errors exceeds or is equal to 1 per minute on average within 5 minutes. The corresponding alarm metric type is**Database metrics**The alarm indicator is**Database call errors**The rule is that the average value in the last five minutes is greater than or equal to 1.

## Create application monitoring-abnormal call alarm

If you need to create an alarm rule that determines whether an application call is abnormal, you can click**Default Alert of Application Monitoring-alert of abnormal calls**Right**Operation**Column**Create an alarm**.

![Db_alarm_exception_invocation](../images/p82391.png)

As shown in the preceding figure, the alarm rule is based on two metrics. An alarm event is generated when one of the conditions is met.

-   Timeout Calls exist: the average time consumed by an application to call an API to the outside is more than or equal to 2 s per minute within 5 minutes. The corresponding alarm metric type is**Application call statistics**The alarm indicator is**Call Response time\_ms**The rule is that the average value in the last five minutes is greater than or equal to 2000.
-   Error calls: the number of API calls provided by an application to the outside exceeds or is equal to once per minute within five minutes. The corresponding alarm metric type is**Application call statistics**The alarm indicator is**Number of call errors**The rule is that the average value in the last five minutes is greater than or equal to 1.

## Create application monitoring-host monitoring alarm

If you need to create an alarm rule that determines whether the ECS instance of the node where the application is located is abnormal, click**Default application monitoring alarms-host monitoring alarms**Right**Operation**Column**Create an alarm**.

![Db_alarm_host_monitor](../images/p82394.png)

As shown in the preceding figure, the alarm rule is based on two metrics. An alarm event is generated when one of the conditions is met.

-   CPU utilization too high: the CPU usage of the machine on the node where the application is located exceeds or is equal to 90% per minute on average within 5 minutes. The corresponding alarm metric type is**Host Monitoring**The alarm indicator is**Cpu\_percentage used by node users**The rule is that the average value in the last five minutes is greater than or equal to 90.
-   Insufficient disk space: the average number of idle disks in the ECS instance of the node where the application is located is less than or equal to one MB per minute within five minutes. The corresponding alarm metric type is**Host Monitoring**The alarm indicator is**Idle disk space on the node \_ byte**The rule is that the average value in the last five minutes is less than or equal to 1048576 \(that is, 1 MB\).

## Create application monitoring-process exception alarm

If you need to create an alarm rule to determine whether the process is abnormal \(the process is alive\), you can click**Default Alert of Application Monitoring-process exception alert**Right**Operation**Column**Create an alarm**.

![Db_alarm_process_exceptionpng](../images/p82395.png)

As shown in the preceding figure, the alarm rule is based on a metric. An alarm event is generated when the condition is met.

-   Process alive: The process is abnormal. The corresponding alarm metric type is**JVM Monitoring**The alarm indicator is**Jvm\_threads**The rule shows that the average value in the last minute exceeds the year-on-year decline rate of the previous hour.

## Create application monitoring-GC exception alarm

If you need to create an alarm rule to determine whether the application has GC exceptions, you can click**Default Alert of Application Monitoring-GC exception alert**Right**Operation**Column**Create an alarm**.

![Db_alarm_gc_exceptionpng](../images/p82422.png)

As shown in the preceding figure, the alarm rule is based on three indicators. An alarm event is generated when the following three conditions are met.

-   Excessive FullGC: An application has more than or equal to 2 FullGC times per minute in 10 minutes. The corresponding alarm metric type is**JVM Monitoring**The alarm indicator is**Jvm\_fullgc count**The rule is that the average value in the last 10 minutes is greater than or equal to 2.
-   FullGC time consumed: the FullGC time consumed by an application exceeds or is equal to 10 s on average per minute within 10 minutes. The corresponding alarm metric type is**JVM Monitoring**The alarm indicator is**Jvm\_fullgc takes \_ms**The rule is that the average value in the last 10 minutes is greater than or equal to 10000 \(that is, 10 s\).
-   YoungGC: the total time consumed by the application&\#39;s YoungGC in one minute exceeds or is equal to 5S. The corresponding alarm metric type is**JVM Monitoring**The alarm indicator is**Jvm\_younggc takes \_ms**The sum of rules for the last minute is greater than or equal to 5000 \(that is, 5S, the threshold value configured here is large, you can adjust according to your needs\).

## Create a browser monitor-JS exception alarm

If you need to create an alarm rule to determine whether the front-end application has JS exceptions, you can click**Default alerts for browser monitoring**Right**Operation**Column**Create an alarm**.

![Db_alarm_js_exception](../images/p82430.png)

As shown in the preceding figure, this alarm rule is based on two metrics. An alarm event is generated when the following two conditions are met.

-   High JS error rate: the JS error rate of the frontend application exceeds or is equal to 20% on average within 10 minutes. The corresponding alarm metric type is**Page metrics**The alarm indicator is**JS error rate**The rule is that the average value in the last 10 minutes is greater than or equal to 0.2 \(20%\).
-   Excessive JS errors: the total number of JS errors of the front-end application in 10 minutes exceeds or is equal to 20. The corresponding alarm metric type is**Page metrics**The alarm indicator is**JS errors**The rule is that the sum of the last 10 minutes is greater than or equal to 20.

## More references

For more information about the fields and**Advanced Configuration**For more information, see[Description of basic fields](/intl.en-US/Dashboard and alerting/Create an alert.md).

