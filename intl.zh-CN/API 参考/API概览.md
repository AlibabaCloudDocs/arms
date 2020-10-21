# API概览

ARMS提供应用监控、前端监控、Prometheus监控、自定义监控和报警的API。本文列出了全部API文档链接及API功能说明。

## 应用监控

|API|描述|
|---|--|
|[ListTraceApps](/intl.zh-CN/API 参考/应用监控/ListTraceApps.md)|获取指定地域下全部应用监控任务的列表。|
|[ConfigApp](/intl.zh-CN/API 参考/应用监控/ConfigApp.md)|打开或关闭应用监控的Agent总开关，或者查询Agent总开关的状态。|
|[DeleteTraceApp](/intl.zh-CN/API 参考/应用监控/DeleteTraceApp.md)|删除应用。|
|[SearchTraceAppByName](/intl.zh-CN/API 参考/应用监控/SearchTraceAppByName.md)|按应用名称查询应用监控任务。|
|[SearchTraceAppByPage](/intl.zh-CN/API 参考/应用监控/SearchTraceAppByPage.md)|分页查询应用监控任务。|
|[SearchTraces](/intl.zh-CN/API 参考/应用监控/SearchTraces.md)|查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。|
|[SearchTracesByPage](/intl.zh-CN/API 参考/应用监控/SearchTracesByPage.md)|分页查询调用链列表信息，可根据时间、应用名称、IP地址、Span名称和Tag等信息筛选调用链。|
|[GetTrace](/intl.zh-CN/API 参考/应用监控/GetTrace.md)|获取调用链详情。|
|[GetMultipleTrace](/intl.zh-CN/API 参考/应用监控/GetMultipleTrace.md)|获取多个调用链的详情。|
|[QueryMetricByPage（应用监控）](/intl.zh-CN/API 参考/应用监控/QueryMetricByPage（应用监控）.md)|分页查询应用监控的相关监控指标。|
|[SaveTraceAppConfig](/intl.zh-CN/API 参考/应用监控/SaveTraceAppConfig.md)|进行应用监控的自定义设置（如调用链采样设置、Agent开关等）。|

## 前端监控

|API|描述|
|---|--|
|[CreateRetcodeApp](/intl.zh-CN/API 参考/前端监控/CreateRetcodeApp.md)|创建前端监控任务。|
|[DeleteRetcodeApp](/intl.zh-CN/API 参考/前端监控/DeleteRetcodeApp.md)|删除前端监控任务。|
|[ListRetcodeApps](/intl.zh-CN/API 参考/前端监控/ListRetcodeApps.md)|获取指定地域下全部前端监控任务的列表。|
|[SearchRetcodeAppByPage](/intl.zh-CN/API 参考/前端监控/SearchRetcodeAppByPage.md)|分页查询前端监控任务。|
|[SetRetcodeShareStatus](/intl.zh-CN/API 参考/前端监控/SetRetcodeShareStatus.md)|打开或关闭前端监控站点的免登录分享开关。|
|[GetRetcodeShareUrl](/intl.zh-CN/API 参考/前端监控/GetRetcodeShareUrl.md)|获取前端监控站点的分享地址。|
|[QueryMetricByPage（前端监控）](/intl.zh-CN/API 参考/前端监控/QueryMetricByPage（前端监控）.md)|分页查询前端监控的相关监控指标。|

## Prometheus监控

|API|描述|
|---|--|
|[AddGrafana](/intl.zh-CN/API 参考/Prometheus监控/AddGrafana.md)|集成ARMS Prometheus监控的大盘。|
|[AddIntegration](/intl.zh-CN/API 参考/Prometheus监控/AddIntegration.md)|集成ARMS Prometheus监控的大盘以及采集规则。|
|[GetPrometheusApiToken](/intl.zh-CN/API 参考/Prometheus监控/GetPrometheusApiToken.md)|获取集成ARMS Prometheus监控所需的Token。|
|[ListDashboards](/intl.zh-CN/API 参考/Prometheus监控/ListDashboards.md)|获取集群的Grafana大盘的列表。|

## 自定义监控

|API|描述|
|---|--|
|[QueryDataset（通用数据集）]()|查询通用数据集中的数据。|
|[QueryDataset（下钻数据集）]()|查询下钻数据集中的数据。|

## 报警

|API|描述|
|---|--|
|[ImportAppAlertRules](/intl.zh-CN/API 参考/报警/ImportAppAlertRules.md)|导入应用监控或前端监控报警规则。|
|[DeleteAlertRules](/intl.zh-CN/API 参考/报警/DeleteAlertRules.md)|删除报警规则。|
|[SearchAlertRules](/intl.zh-CN/API 参考/报警/SearchAlertRules.md)|查询报警规则。|
|[StartAlert](/intl.zh-CN/API 参考/报警/StartAlert.md)|启动报警规则。|
|[StopAlert](/intl.zh-CN/API 参考/报警/StopAlert.md)|停止报警规则。|
|[CreateAlertContact](/intl.zh-CN/API 参考/报警/CreateAlertContact.md)|创建报警联系人。|
|[DeleteAlertContact](/intl.zh-CN/API 参考/报警/DeleteAlertContact.md)|删除报警联系人。|
|[UpdateAlertContact](/intl.zh-CN/API 参考/报警/UpdateAlertContact.md)|更新报警联系人。|
|[SearchAlertContact](/intl.zh-CN/API 参考/报警/SearchAlertContact.md)|查询报警联系人。|
|[CreateAlertContactGroup](/intl.zh-CN/API 参考/报警/CreateAlertContactGroup.md)|创建报警联系人分组。|
|[DeleteAlertContactGroup](/intl.zh-CN/API 参考/报警/DeleteAlertContactGroup.md)|删除报警联系人分组。|
|[UpdateAlertContactGroup](/intl.zh-CN/API 参考/报警/UpdateAlertContactGroup.md)|更新报警联系人分组。|
|[SearchAlertContactGroup](/intl.zh-CN/API 参考/报警/SearchAlertContactGroup.md)|查询报警联系人分组。|
|[SearchAlertHistories](/intl.zh-CN/API 参考/报警/SearchAlertHistories.md)|查询报警规则的报警发送记录。|
|[SearchEvents](/intl.zh-CN/API 参考/报警/SearchEvents.md)|查询报警事件记录。|

