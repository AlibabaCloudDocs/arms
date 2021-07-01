# List of API operations by feature

Application Real-Time Monitoring Service \(ARMS\) provides API operations for application monitoring, frontend monitoring, Prometheus monitoring, business monitoring, access control, and alerting. The following tables list API operations available for use in ARMS.

## Application monitoring

|API operation|Description|
|-------------|-----------|
|[ConfigApp](/intl.en-US/API Reference/Application monitoring/ConfigApp.md)|Turns on or off the main switch of an ARMS agent, or queries the status of the main switch.|
|[DeleteTraceApp](/intl.en-US/API Reference/Application monitoring/DeleteTraceApp.md)|Deletes an application based on a specified process identifier \(PID\) and type.|
|[ListTraceApps](/intl.en-US/API Reference/Application monitoring/ListTraceApps.md)|Queries all application monitoring jobs in a specified region.|
|[GetTraceApp](/intl.en-US/API Reference/Application monitoring/GetTraceApp.md)|Queries the details of an application monitoring job.|
|[GetAppApiByPage](/intl.en-US/API Reference/Application monitoring/GetAppApiByPage.md)|Queries the APIs of frontend monitoring by page.|
|[SearchTraceAppByName](/intl.en-US/API Reference/Application monitoring/SearchTraceAppByName.md)|Queries application monitoring jobs by application name.|
|[SearchTraceAppByPage](/intl.en-US/API Reference/Application monitoring/SearchTraceAppByPage.md)|Queries application monitoring jobs by page.|
|[SearchTraces](/intl.en-US/API Reference/Application monitoring/SearchTraces.md)|Queries traces. You can filter traces by time range, application name, IP address, span name, and tag.|
|[SearchTracesByPage](/intl.en-US/API Reference/Application monitoring/SearchTracesByPage.md)|Queries traces by page. You can filter traces by time range, application name, IP address, span name, and tag.|
|[GetTrace](/intl.en-US/API Reference/Application monitoring/GetTrace.md)|Queries the detailed information of a trace.|
|[GetMultipleTrace](/intl.en-US/API Reference/Application monitoring/GetMultipleTrace.md)|Queries the detailed information of multiple traces.|
|[QueryMetricByPage \(Application Monitoring\)](/intl.en-US/API Reference/Application monitoring/QueryMetricByPage (Application Monitoring).md)|Queries the monitoring metrics of application monitoring by page.|
|[SaveTraceAppConfig](/intl.en-US/API Reference/Application monitoring/SaveTraceAppConfig.md)|Customizes application monitoring settings, such as trace sampling and agent switch settings.|
|[DescribeTraceLicenseKey](/intl.en-US/API Reference/Application monitoring/DescribeTraceLicenseKey.md)|Queries the license key for application monitoring.|
|[GetAgentDownloadUrl](/intl.en-US/API Reference/Application monitoring/GetAgentDownloadUrl.md)|Obtains the download URL of an ARMS agent.|

## Frontend monitoring

|API operation|Description|
|-------------|-----------|
|[CreateRetcodeApp](/intl.en-US/API Reference/Browser monitoring/CreateRetcodeApp.md)|Creates a frontend monitoring job for an application.|
|[DeleteRetcodeApp](/intl.en-US/API Reference/Browser monitoring/DeleteRetcodeApp.md)|Deletes a frontend monitoring job.|
|[ListRetcodeApps](/intl.en-US/API Reference/Browser monitoring/ListRetcodeApps.md)|Queries all frontend monitoring jobs in a specified region.|
|[SearchRetcodeAppByPage](/intl.en-US/API Reference/Browser monitoring/SearchRetcodeAppByPage.md)|Queries frontend monitoring jobs for applications by page.|
|[SetRetcodeShareStatus](/intl.en-US/API Reference/Browser monitoring/SetRetcodeShareStatus.md)|Turns on or off the logon-free sharing switch for an application monitored by the frontend monitoring feature.|
|[GetRetcodeShareUrl](/intl.en-US/API Reference/Browser monitoring/GetRetcodeShareUrl.md)|Queries the sharing URL at the frontend monitoring site.|
|[t1951300.md\#](/intl.en-US/API Reference/Browser monitoring/QueryMetricByPage (Browser Monitoring).md)|Queries the monitoring metrics of frontend monitoring by page.|

## Prometheus monitoring

|API operation|Description|
|-------------|-----------|
|[AddGrafana](/intl.en-US/API Reference/Prometheus/AddGrafana.md)|Integrates a dashboard for ARMS Prometheus.|
|[AddIntegration](/intl.en-US/API Reference/Prometheus/AddIntegration.md)|Integrates a dashboard and data collection rules for ARMS Prometheus.|
|[GetPrometheusApiToken](/intl.en-US/API Reference/Prometheus/GetPrometheusApiToken.md)|Queries the token required to integrate ARMS Prometheus.|
|[ListDashboards](/intl.en-US/API Reference/Prometheus/ListDashboards.md)|Queries the Grafana dashboards of a Container Service for Kubernetes cluster.|
|[CreatePrometheusAlertRule](/intl.en-US/API Reference/Prometheus/CreatePrometheusAlertRule.md)|Creates an alert rule.|
|[UpdatePrometheusAlertRule](/intl.en-US/API Reference/Prometheus/UpdatePrometheusAlertRule.md)|Updates an alert rule.|
|[ListPrometheusAlertRules](/intl.en-US/API Reference/Prometheus/ListPrometheusAlertRules.md)|Queries the alert rules of ARMS Prometheus.|
|[DescribePrometheusAlertRule](/intl.en-US/API Reference/Prometheus/DescribePrometheusAlertRule.md)|Queries the details of an alert rule of ARMS Prometheus.|
|[DeletePrometheusAlertRule](/intl.en-US/API Reference/Prometheus/DeletePrometheusAlertRule.md)|Deletes an alert rule of ARMS Prometheus.|
|[ListPrometheusAlertTemplates](/intl.en-US/API Reference/Prometheus/ListPrometheusAlertTemplates.md)|Queries the alert templates of ARMS Prometheus.|
|[ListActivatedAlerts](/intl.en-US/API Reference/Prometheus/ListActivatedAlerts.md)|Queries the alerts that have been triggered.|

## Business monitoring

|API operation|Description|
|-------------|-----------|
|[ApplyScenario](/intl.en-US/API Reference/Business monitoring/ApplyScenario.md)|Creates or updates a business monitoring job.|
|[ListScenario](/intl.en-US/API Reference/Business monitoring/ListScenario.md)|Queries the detailed information of a business monitoring job.|
|[DeleteScenario](/intl.en-US/API Reference/Business monitoring/DeleteScenario.md)|Deletes a business monitoring job.|

## Access control

|API operation|Description|
|-------------|-----------|
|[OpenXtraceDefaultSLR](/intl.en-US/API Reference/Access control/OpenXtraceDefaultSLR.md)|Activates the service-linked role AliyunServiceRoleForXtrace for Tracing Analysis.|
|[OpenArmsDefaultSLR](/intl.en-US/API Reference/Access control/OpenArmsDefaultSLR.md)|Activates the service-linked role AliyunServiceRoleForARMS for ARMS.|

## Alerting

|API operation|Description|
|-------------|-----------|
|[ImportAppAlertRules](/intl.en-US/API Reference/Alerting/ImportAppAlertRules.md)|Creates an alert rule based on an alert template.|
|[DeleteAlertRules](/intl.en-US/API Reference/Alerting/DeleteAlertRules.md)|Deletes one or more alert rules.|
|[SearchAlertRules](/intl.en-US/API Reference/Alerting/SearchAlertRules.md)|Queries alert rules.|
|[StartAlert](/intl.en-US/API Reference/Alerting/StartAlert.md)|Enables an alert rule.|
|[StopAlert](/intl.en-US/API Reference/Alerting/StopAlert.md)|Disables an alert rule.|
|[CreateAlertContact](/intl.en-US/API Reference/Alerting/CreateAlertContact.md)|Creates an alert contact.|
|[DeleteAlertContact](/intl.en-US/API Reference/Alerting/DeleteAlertContact.md)|Deletes an alert contact.|
|[UpdateAlertContact](/intl.en-US/API Reference/Alerting/UpdateAlertContact.md)|Modifies an alert contact.|
|[SearchAlertContact](/intl.en-US/API Reference/Alerting/SearchAlertContact.md)|Queries alert contacts.|
|[CreateAlertContactGroup](/intl.en-US/API Reference/Alerting/CreateAlertContactGroup.md)|Creates an alert contact group.|
|[DeleteAlertContactGroup](/intl.en-US/API Reference/Alerting/DeleteAlertContactGroup.md)|Deletes an alert contact group.|
|[UpdateAlertContactGroup](/intl.en-US/API Reference/Alerting/UpdateAlertContactGroup.md)|Modifies an alert contact group.|
|[SearchAlertContactGroup](/intl.en-US/API Reference/Alerting/SearchAlertContactGroup.md)|Queries alert contact groups.|
|[SearchAlertHistories](/intl.en-US/API Reference/Alerting/SearchAlertHistories.md)|Queries the alert records of an alert rule.|
|[SearchEvents](/intl.en-US/API Reference/Alerting/SearchEvents.md)|Queries alert event records.|
|[CreateDispatchRule](/intl.en-US/API Reference/Alerting/CreateDispatchRule.md)|Creates a dispatch policy.|
|[DescribeDispatchRule](/intl.en-US/API Reference/Alerting/DescribeDispatchRule.md)|Queries the information of a dispatch policy.|
|[UpdateDispatchRule](/intl.en-US/API Reference/Alerting/UpdateDispatchRule.md)|Modifies a dispatch policy.|
|[DeleteDispatchRule](/intl.en-US/API Reference/Alerting/DeleteDispatchRule.md)|Deletes a dispatch policy based on a specified ID.|

