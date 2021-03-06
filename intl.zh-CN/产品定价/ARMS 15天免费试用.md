# ARMS 15天免费试用

应用实时监控服务ARMS试用版提供应用监控、前端监控和Prometheus监控的免费试用。本文介绍ARMS试用版的使用规则。

关于ARMS试用版和专家版的对比，请参见[产品版本对比](/intl.zh-CN/产品定价/产品版本对比.md)。

-   应用监控试用版：有效期至开通后第15日的00:00截止。在此期间，每天的免费额度为240 Agent×Hour（例如10个Agent分别运行24小时）。

    **说明：** 一个Agent可以监控一个应用实例，例如一个Tomcat实例或一个Java进程。

-   前端监控试用版：有效期至开通后第15日的00:00截止。在此期间，每天的免费额度为20000次数据上报。
-   Prometheus监控试用版：有效期至开通后第15日的00:00截止。在此期间，每天可免费上报200万条自定义指标。

## 注意事项

-   应用监控：流量按照实际所有应用在线时间总长计算，按天结算。 应用监控数据默认缓存60天。
-   前端监控：计费计量主要为页面PV调用和API调用上报次数，自定义上报次数。按天结算，不足1000上报次数部分按1000算。例如，1350次上报视为2000次上报。 前端监控数据默认缓存30天。
-   前端监控每日上报流量的计算公式：每日上报流量=每天PV+\(每天API调用次数-50万\)\*0.1+自定义上报次数。
-   Prometheus监控：指标分为基础指标和自定义指标。Prometheus监控数据默认缓存15天。
-   不开通专家版则不收费。如果您没有开通专家版，则配额用完后服务将停止，您可第二天手动或设置自动开启监控服务。关闭和重启监控服务不影响您的应用正常运行。
-   免费试用版会每天0点重置配额，当天有效。

