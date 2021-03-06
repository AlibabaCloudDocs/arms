# API概览

ARMS提供应用监控、前端监控、Prometheus监控、业务监控、自定义监控、访问控制和报警的API。本文列出了全部API文档链接及API功能说明。

## 应用监控

|API|描述|
|---|--|
|[ConfigApp](/cn.zh-CN/API参考/应用监控/ConfigApp.md)|打开或关闭应用监控的Agent总开关，或者查询Agent总开关的状态。|
|[DeleteTraceApp](/cn.zh-CN/API参考/应用监控/DeleteTraceApp.md)|删除应用。|
|[ListTraceApps](/cn.zh-CN/API参考/应用监控/ListTraceApps.md)|获取指定地域下全部应用监控任务的列表。|
|[GetTraceApp](/cn.zh-CN/API参考/应用监控/GetTraceApp.md)|获取应用监控任务详情。|
|[GetAppApiByPage](/cn.zh-CN/API参考/应用监控/GetAppApiByPage.md)|分页查询前端应用接口数据。|
|[SearchTraceAppByName](/cn.zh-CN/API参考/应用监控/SearchTraceAppByName.md)|按应用名称查询应用监控任务。|
|[SearchTraceAppByPage](/cn.zh-CN/API参考/应用监控/SearchTraceAppByPage.md)|分页查询应用监控任务。|
|[SearchTraces](/cn.zh-CN/API参考/应用监控/SearchTraces.md)|查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。|
|[SearchTracesByPage](/cn.zh-CN/API参考/应用监控/SearchTracesByPage.md)|分页查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。|
|[GetTrace](/cn.zh-CN/API参考/应用监控/GetTrace.md)|获取调用链详情。|
|[GetMultipleTrace](/cn.zh-CN/API参考/应用监控/GetMultipleTrace.md)|获取多个调用链的详情。|
|[QueryMetricByPage（应用监控）](/cn.zh-CN/API参考/应用监控/QueryMetricByPage（应用监控）.md)|分页查询应用监控的相关监控指标。|
|[SaveTraceAppConfig](/cn.zh-CN/API参考/应用监控/SaveTraceAppConfig.md)|进行应用监控的自定义设置（如调用链采样设置、Agent开关等）。|
|[DescribeTraceLicenseKey](/cn.zh-CN/API参考/应用监控/DescribeTraceLicenseKey.md)|列出LicenseKey。|
|[GetAgentDownloadUrl](/cn.zh-CN/API参考/应用监控/GetAgentDownloadUrl.md)|获取探针下载链接。|

## 前端监控

|API|描述|
|---|--|
|[CreateRetcodeApp](/cn.zh-CN/API参考/前端监控/CreateRetcodeApp.md)|创建前端监控任务。|
|[DeleteRetcodeApp](/cn.zh-CN/API参考/前端监控/DeleteRetcodeApp.md)|删除前端监控任务。|
|[ListRetcodeApps](/cn.zh-CN/API参考/前端监控/ListRetcodeApps.md)|获取指定地域下全部前端监控任务的列表。|
|[SearchRetcodeAppByPage](/cn.zh-CN/API参考/前端监控/SearchRetcodeAppByPage.md)|分页查询前端监控任务。|
|[SetRetcodeShareStatus](/cn.zh-CN/API参考/前端监控/SetRetcodeShareStatus.md)|打开或关闭前端监控站点的免登录分享开关。|
|[GetRetcodeShareUrl](/cn.zh-CN/API参考/前端监控/GetRetcodeShareUrl.md)|获取前端监控站点的分享地址。|
|[QueryMetricByPage（前端监控）](/cn.zh-CN/API参考/前端监控/QueryMetricByPage（前端监控）.md)|分页查询前端监控的相关监控指标。|

## Prometheus监控

|API|描述|
|---|--|
|[AddGrafana](/cn.zh-CN/API参考/Prometheus监控/AddGrafana.md)|集成ARMS Prometheus监控的大盘。|
|[AddIntegration](/cn.zh-CN/API参考/Prometheus监控/AddIntegration.md)|集成ARMS Prometheus监控的大盘以及采集规则。|
|[GetPrometheusApiToken](/cn.zh-CN/API参考/Prometheus监控/GetPrometheusApiToken.md)|获取集成ARMS Prometheus监控所需的Token。|
|[ListDashboards](/cn.zh-CN/API参考/Prometheus监控/ListDashboards.md)|获取集群的Grafana大盘的列表。|
|[CreatePrometheusAlertRule](/cn.zh-CN/API参考/Prometheus监控/CreatePrometheusAlertRule.md)|创建告警规则。|
|[UpdatePrometheusAlertRule](/cn.zh-CN/API参考/Prometheus监控/UpdatePrometheusAlertRule.md)|更新告警规则。|
|[ListPrometheusAlertRules](/cn.zh-CN/API参考/Prometheus监控/ListPrometheusAlertRules.md)|查看Prometheus告警规则列表。|
|[DescribePrometheusAlertRule](/cn.zh-CN/API参考/Prometheus监控/DescribePrometheusAlertRule.md)|查看Prometheus告警规则。|
|[DeletePrometheusAlertRule](/cn.zh-CN/API参考/Prometheus监控/DeletePrometheusAlertRule.md)|删除Prometheus告警规则。|
|[ListPrometheusAlertTemplates](/cn.zh-CN/API参考/Prometheus监控/ListPrometheusAlertTemplates.md)|查看Prometheus告警模板列表。|
|[ListActivatedAlerts](/cn.zh-CN/API参考/Prometheus监控/ListActivatedAlerts.md)|查询已经触发的告警列表。|

## 业务监控

|API|描述|
|---|--|
|[ApplyScenario](/cn.zh-CN/API参考/业务监控/ApplyScenario.md)|创建或更新业务监控。|
|[ListScenario](/cn.zh-CN/API参考/业务监控/ListScenario.md)|获取业务监控详细信息。|
|[DeleteScenario](/cn.zh-CN/API参考/业务监控/DeleteScenario.md)|删除业务监控。|

## 自定义监控

|API|描述|
|---|--|
|[QueryDataset（通用数据集）](/cn.zh-CN/API参考/自定义监控/QueryDataset（通用数据集）.md)|查询通用数据集中的数据。|
|[QueryDataset（下钻数据集）](/cn.zh-CN/API参考/自定义监控/QueryDataset（下钻数据集）.md)|查询下钻数据集中的数据。|

## 访问控制

|API|描述|
|---|--|
|[OpenXtraceDefaultSLR](/cn.zh-CN/API参考/访问控制/OpenXtraceDefaultSLR.md)|开通链路追踪服务关联角色AliyunServiceRoleForXtrace。|
|[OpenArmsDefaultSLR](/cn.zh-CN/API参考/访问控制/OpenArmsDefaultSLR.md)|开通ARMS服务关联角色AliyunServiceRoleForARMS。|

## 报警

|API|描述|
|---|--|
|[ImportAppAlertRules](/cn.zh-CN/API参考/报警/ImportAppAlertRules.md)|导入应用监控或前端监控报警规则。|
|[DeleteAlertRules](/cn.zh-CN/API参考/报警/DeleteAlertRules.md)|删除报警规则。|
|[SearchAlertRules](/cn.zh-CN/API参考/报警/SearchAlertRules.md)|查询报警规则。|
|[StartAlert](/cn.zh-CN/API参考/报警/StartAlert.md)|启动报警规则。|
|[StopAlert](/cn.zh-CN/API参考/报警/StopAlert.md)|停止报警规则。|
|[CreateAlertContact](/cn.zh-CN/API参考/报警/CreateAlertContact.md)|创建报警联系人。|
|[DeleteAlertContact](/cn.zh-CN/API参考/报警/DeleteAlertContact.md)|删除报警联系人。|
|[UpdateAlertContact](/cn.zh-CN/API参考/报警/UpdateAlertContact.md)|更新报警联系人。|
|[SearchAlertContact](/cn.zh-CN/API参考/报警/SearchAlertContact.md)|查询报警联系人。|
|[CreateAlertContactGroup](/cn.zh-CN/API参考/报警/CreateAlertContactGroup.md)|创建报警联系人分组。|
|[DeleteAlertContactGroup](/cn.zh-CN/API参考/报警/DeleteAlertContactGroup.md)|删除报警联系人分组。|
|[UpdateAlertContactGroup](/cn.zh-CN/API参考/报警/UpdateAlertContactGroup.md)|更新报警联系人分组。|
|[SearchAlertContactGroup](/cn.zh-CN/API参考/报警/SearchAlertContactGroup.md)|查询报警联系人分组。|
|[SearchAlertHistories](/cn.zh-CN/API参考/报警/SearchAlertHistories.md)|查询报警规则的报警发送记录。|
|[SearchEvents](/cn.zh-CN/API参考/报警/SearchEvents.md)|查询报警事件记录。|
|[CreateDispatchRule](/cn.zh-CN/API参考/报警/CreateDispatchRule.md)|创建分派策略。|
|[DescribeDispatchRule](/cn.zh-CN/API参考/报警/DescribeDispatchRule.md)|查询分派策略信息。|
|[UpdateDispatchRule](/cn.zh-CN/API参考/报警/UpdateDispatchRule.md)|修改分派策略。|
|[DeleteDispatchRule](/cn.zh-CN/API参考/报警/DeleteDispatchRule.md)|删除指定ID的分派策略。|

