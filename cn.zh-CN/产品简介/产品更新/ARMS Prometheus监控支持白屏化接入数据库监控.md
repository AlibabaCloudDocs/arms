# ARMS Prometheus监控支持白屏化接入数据库监控

ARMS Prometheus监控于2020年3月20日发布全新升级特性，即支持一键接入Redis、MySQL、ElasticSearch和MangoDB等数据库监控，并提供开箱即用的监控大盘。

**说明：** ARMS Prometheus监控提供15天免费试用期，在[云产品开通页](https://common-buy.aliyun.com/?&commodityCode=arms#/open)开通ARMS Prometheus监控免费试用。您也可以加入产品免费试用钉钉群：23155358。

## ARMS Prometheus监控介绍

ARMS Prometheus监控服务提供了一站式开箱即用的Prometheus监控能力，其特点如下所示：

-   精简稳定的Prometheus采集器：Prometheus采集器通过Helm Chart方式部署在用户集群，基于Prometheus Server精简并优化功能，专注服务发现和数据采集，资源消耗相比Prometheus Server降至二十分之一，并且支持水平扩展。
-   稳定大容量的云存储：云存储基于阿里云的日志服务，提供接近无上限的存储空间和高效稳定的分布式存储。
-   高效且强大的云端数据查询能力：通过部署在云端的Prometheus服务器提供完全兼容PromQL的指标查询能力，增加下推采样和长时间查询优化功能。
-   默认告警服务：支持原生Alerting Rule， 并默认集成钉钉、邮件等告警通道，打通云上告警联系人通道。
-   开箱即用的Grafana云服务监控大盘：默认提供K8s集群的监控大盘，包含主机、Pod、Deployment、API Server、Ingress和coreDNS等各组件监控大盘，并提供各种三方组件的监控大盘。

了解更多ARMS Prometheus监控内容，请参见[什么是Prometheus监控？]()。

## 一键接入数据库监控

ARMS Prometheus监控服务支持一键接入各种数据库的监控，仅需三步即可看到数据库监控的大盘。

1.  选择监控的数据库类别。

    目前支持Redis、MySQL、ElasticSearch和MangoDB数据库。

    ![pg_prom_choose_database](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2762684951/p94349.png)

2.  输入需要监控的数据库的相应参数。

    以MangoDB数据库为例，输入Exporter名称，以及需要监控的MangoDB数据库的地址、端口号、用户名和密码。

    ![pg_prom_exporter_setting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2762684951/p94350.png)

3.  找到新接入的Exporter并查看相应的监控大盘。

    ![pg_prom_mongodb_dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2762684951/p94351.png)


ARMS Prometheus监控服务提供了白屏化安装配置Exporter的能力，并提供开箱即用的专属监控大盘。目前支持大部分主流的数据库组件，后续会接入更多应用组件，敬请期待。

**相关文档**  


[什么是Prometheus监控？]()

