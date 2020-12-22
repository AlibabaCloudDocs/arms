# API Overview

Application Real-Time Monitoring Service \(ARMS\) provides APIs for application monitoring, browser monitoring, Prometheus Service, custom monitoring, and alerting. This topic lists all the API documentation links and describes each API operation.

## Application monitoring

|API|Description|
|---|-----------|
|[ListTraceApps](/intl.en-US/API reference/Application monitoring/ListTraceApps.md)|Queries the list of all application monitoring tasks in a specified region.|
|[ConfigApp]()|Turns on or off the Probe Master Switch of the application monitoring agent, or queries the status of the Probe Master Switch of the agent.|
|[DeleteTraceApp]()|Deletes an application from the application list.|
|[SearchTraceAppByName](/intl.en-US/API reference/Application monitoring/SearchTraceAppByName.md)|Queries application monitoring tasks by application name.|
|[SearchTraceAppByPage](/intl.en-US/API reference/Application monitoring/SearchTraceAppByPage.md)|Queries application monitoring tasks by page.|
|[SearchTraces](/intl.en-US/API reference/Application monitoring/SearchTraces.md)|Queries the list of traces. You can filter traces by time range, application name, IP address, span name, and tag.|
|[SearchTracesByPage](/intl.en-US/API reference/Application monitoring/SearchTracesByPage.md)|Queries traces by page. You can filter traces by time range, application name, IP address, span name, and tag.|
|[GetTrace](/intl.en-US/API reference/Application monitoring/GetTrace.md)|Queries detailed information of a trace.|
|[GetMultipleTrace]()|Queries detailed information of multiple traces.|
|[QueryMetricByPage \(Application Monitoring\)](/intl.en-US/API reference/Application monitoring/QueryMetricByPage (Application Monitoring).md)|Queries the monitoring metrics of application monitoring by page.|
|[SaveTraceAppConfig](/intl.en-US/API reference/Application monitoring/SaveTraceAppConfig.md)|Customizes application monitoring settings, such as trace sampling and agent switches.|

## Browser monitoring

|API|Description|
|---|-----------|
|[CreateRetcodeApp](/intl.en-US/API reference/Browser monitoring/CreateRetcodeApp.md)|Creates a browser monitoring task.|
|[DeleteRetcodeApp](/intl.en-US/API reference/Browser monitoring/DeleteRetcodeApp.md)|Deletes a browser monitoring task.|
|[ListRetcodeApps](/intl.en-US/API reference/Browser monitoring/ListRetcodeApps.md)|Queries the list of all browser monitoring tasks in a specified region.|
|[SearchRetcodeAppByPage](/intl.en-US/API reference/Browser monitoring/SearchRetcodeAppByPage.md)|Queries browser monitoring tasks by page.|
|[SetRetcodeShareStatus](/intl.en-US/API reference/Browser monitoring/SetRetcodeShareStatus.md)|Enables or disables the logon-free sharing switch of a browser monitoring site.|
|[GetRetcodeShareUrl](/intl.en-US/API reference/Browser monitoring/GetRetcodeShareUrl.md)|Queries the sharing URL of a browser monitoring site.|
|[QueryMetricByPage \(Browser Monitoring\)](/intl.en-US/API reference/Browser monitoring/QueryMetricByPage (Browser Monitoring).md)|Queries the monitoring metrics of browser monitoring by page.|

## Prometheus Monitoring

|API|Description|
|---|-----------|
|[AddGrafana](/intl.en-US/API reference/Prometheus监控/AddGrafana.md)|Integrates a dashboard for ARMS Prometheus Service.|
|[AddIntegration](/intl.en-US/API reference/Prometheus监控/AddIntegration.md)|Integrates a dashboard and data collection rules for ARMS Prometheus Service.|
|[GetPrometheusApiToken](/intl.en-US/API reference/Prometheus监控/GetPrometheusApiToken.md)|Queries the token required to integrate Prometheus Service.|
|[ListDashboards](/intl.en-US/API reference/Prometheus监控/ListDashboards.md)|Queries the list of Grafana dashboards for a cluster.|

## Alert

|API|Description|
|---|-----------|
|[ImportAppAlertRules](/intl.en-US/API reference/Alerts/ImportAppAlertRules.md)|Imports alert rules from application monitoring or browser monitoring.|
|[t1858119.md\#]()|Deletes one or more alert rules.|
|[t1858183.md\#]()|Queries alert rules.|
|[t1917839.md\#]()|Enables an alert rule.|
|[t1917838.md\#]()|Disables an alert rule.|
|[CreateAlertContact](/intl.en-US/API reference/Alerts/CreateAlertContact.md)|Creates an alert contact.|
|[t1858116.md\#]()|Deletes an alert contact.|
|[t1917348.md\#]()|Modifies an alert contact.|
|[SearchAlertContact](/intl.en-US/API reference/Alerts/SearchAlertContact.md)|Queries alert contacts.|
|[CreateAlertContactGroup](/intl.en-US/API reference/Alerts/CreateAlertContactGroup.md)|Creates an alert contact group.|
|[t1858118.md\#]()|Deletes an alert contact group.|
|[t1917377.md\#]()|Modifies an alert contact group.|
|[SearchAlertContactGroup](/intl.en-US/API reference/Alerts/SearchAlertContactGroup.md)|Queries an alert contact group.|
|[t1858153.md\#]()|Queries the alert notifications of an alert rule.|
|[t1858186.md\#]()|Queries alert events.|

