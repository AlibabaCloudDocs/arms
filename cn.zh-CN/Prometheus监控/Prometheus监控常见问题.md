---
keyword: [Prometheus监控, 常见问题, 集成]
---

# Prometheus监控常见问题

本章节汇总了使用阿里云Prometheus监控的常见问题。

## Grafana、Istio和HPA等第三方系统如何集成Prometheus监控？

Grafana、Istio和HPA等第三方系统集成Prometheus监控时，需要获取Prometheus监控的API接口地址。可以按照以下操作步骤获取API接口地址：

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在**设置**页面顶部单击**Agent设置**。

5.  在**Agent设置**页签上，复制**步骤2：API接口地址**后的地址。

    ![pg_pm_settings_tab_agent_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4584298951/p103094.png)


获取到API接口地址后，将其添加到Grafana、Istio和HPA等第三方系统中，即可集成Prometheus监控。完整的Grafana集成Prometheus监控的操作请参见[将阿里云Prometheus监控数据接入本地Grafana]()。

**相关文档**  


[将阿里云Prometheus监控数据接入本地Grafana]()

