# List of operations by function

Application Real-Time Monitoring Service \(ARMS\) provides APIs for application monitoring, frontend monitoring, Prometheus monitoring, and customized monitoring and alerting. The following tables list API operations available for use in ARMS.

## Application monitoring

|API|Description|
|---|-----------|
|[ListTraceApps](/intl.en-US/API Reference/Application monitoring/ListTraceApps.md)|Queries all application monitoring tasks in a specified region.|
|[ConfigApp](/intl.en-US/API Reference/Application monitoring/ConfigApp.md)|Turns on or off the main switch of the application monitoring agent, or queries the main switch status of the agent.|
|[DeleteTraceApp](/intl.en-US/API Reference/Application monitoring/DeleteTraceApp.md)|Deletes an application.|
|[SearchTraceAppByName](/intl.en-US/API Reference/Application monitoring/SearchTraceAppByName.md)|Queries application monitoring tasks by application name.|
|[SearchTraceAppByPage](/intl.en-US/API Reference/Application monitoring/SearchTraceAppByPage.md)|Queries application monitoring tasks by page.|
|[SearchTraces](/intl.en-US/API Reference/Application monitoring/SearchTraces.md)|Queries traces. You can filter traces by time range, application name, IP address, span name, and tag.|
|[SearchTracesByPage](/intl.en-US/API Reference/Application monitoring/SearchTracesByPage.md)|Queries traces by page. You can filter traces by time range, application name, IP address, span name, and tag.|
|[GetTrace](/intl.en-US/API Reference/Application monitoring/GetTrace.md)|Queries the detailed information of a trace.|
|[GetMultipleTrace](/intl.en-US/API Reference/Application monitoring/GetMultipleTrace.md)|Queries detailed information of multiple traces.|
|[QueryMetricByPage \(Application Monitoring\)](/intl.en-US/API Reference/Application monitoring/QueryMetricByPage (Application Monitoring).md)|Queries the monitoring metrics of application monitoring by page.|
|[SaveTraceAppConfig](/intl.en-US/API Reference/Application monitoring/SaveTraceAppConfig.md)|Customizes application monitoring settings, such as trace sampling and agent switches.|

## Browser monitoring

|API|Description|
|---|-----------|
|[CreateRetcodeApp](/intl.en-US/API Reference/Browser monitoring/CreateRetcodeApp.md)|Creates a frontend monitoring task.|
|[DeleteRetcodeApp](/intl.en-US/API Reference/Browser monitoring/DeleteRetcodeApp.md)|Deletes a frontend monitoring task.|
|[ListRetcodeApps](/intl.en-US/API Reference/Browser monitoring/ListRetcodeApps.md)|Queries all frontend monitoring tasks in a specified region.|
|[SearchRetcodeAppByPage](/intl.en-US/API Reference/Browser monitoring/SearchRetcodeAppByPage.md)|Queries frontend monitoring tasks by page.|
|[SetRetcodeShareStatus](/intl.en-US/API Reference/Browser monitoring/SetRetcodeShareStatus.md)|Turns on or off the logon-free sharing switch of a frontend monitoring site.|
|[GetRetcodeShareUrl](/intl.en-US/API Reference/Browser monitoring/GetRetcodeShareUrl.md)|Queries the shared URL of a frontend monitoring site.|
|[QueryMetricByPage \(Browser Monitoring\)](/intl.en-US/API Reference/Browser monitoring/QueryMetricByPage (Browser Monitoring).md)|Queries frontend monitoring metrics by page.|

## Prometheus Monitoring

|API|Description|
|---|-----------|
|[AddGrafana](/intl.en-US/API Reference/Prometheus/AddGrafana.md)|Integrates a dashboard for ARMS Prometheus.|
|[AddIntegration](/intl.en-US/API Reference/Prometheus/AddIntegration.md)|Integrates a dashboard and data collection rules for ARMS Prometheus.|
|[GetPrometheusApiToken](/intl.en-US/API Reference/Prometheus/GetPrometheusApiToken.md)|Queries the token required to integrate Prometheus.|
|[ListDashboards](/intl.en-US/API Reference/Prometheus/ListDashboards.md)|Queries Grafana dashboards of a cluster.|

## Alert

|API|Description|
|---|-----------|
|[ImportAppAlertRules](/intl.en-US/API Reference/Alerting/ImportAppAlertRules.md)|Imports alert rules from application monitoring or frontend monitoring.|
|[DeleteAlertRules](/intl.en-US/API Reference/Alerting/DeleteAlertRules.md)|Deletes one or more alert rules.|
|[SearchAlertRules](/intl.en-US/API Reference/Alerting/SearchAlertRules.md)|Queries alert rules.|
|[StartAlert](/intl.en-US/API Reference/Alerting/StartAlert.md)|Starts an alert rule.|
|[StopAlert](/intl.en-US/API Reference/Alerting/StopAlert.md)|Stops an alert rule.|
|[CreateAlertContact](/intl.en-US/API Reference/Alerting/CreateAlertContact.md)|Creates an alert contact.|
|[DeleteAlertContact](/intl.en-US/API Reference/Alerting/DeleteAlertContact.md)|Deletes an alert contact.|
|[UpdateAlertContact](/intl.en-US/API Reference/Alerting/UpdateAlertContact.md)|Modifies an alert contact.|
|[SearchAlertContact](/intl.en-US/API Reference/Alerting/SearchAlertContact.md)|Queries alert contacts.|
|[CreateAlertContactGroup](/intl.en-US/API Reference/Alerting/CreateAlertContactGroup.md)|Creates an alert contact group.|
|[DeleteAlertContactGroup](/intl.en-US/API Reference/Alerting/DeleteAlertContactGroup.md)|Deletes an alert contact group.|
|[UpdateAlertContactGroup](/intl.en-US/API Reference/Alerting/UpdateAlertContactGroup.md)|Modifies an alert contact group.|
|[SearchAlertContactGroup](/intl.en-US/API Reference/Alerting/SearchAlertContactGroup.md)|Queries an alert contact group.|
|[SearchAlertHistories](/intl.en-US/API Reference/Alerting/SearchAlertHistories.md)|Queries the alert notifications of an alert rule.|
|[SearchEvents](/intl.en-US/API Reference/Alerting/SearchEvents.md)|Queries alert events.|

