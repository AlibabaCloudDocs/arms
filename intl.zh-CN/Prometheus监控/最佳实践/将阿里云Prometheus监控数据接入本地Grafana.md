---
keyword: [Prometheus, Grafana, 本地]
---

# 将阿里云Prometheus监控数据接入本地Grafana

如果您需要在本地的Grafana系统中查看阿里云Prometheus监控数据，可以利用Prometheus监控提供的专用API接口轻松实现此目的。本文介绍了将Prometheus监控数据接入本地Grafana的实现方法。

-   您已成功安装Prometheus监控Agent，请参见[容器服务Kubernetes版集群]()。
-   您已在本地成功安装Grafana软件，请参见[Grafana](https://grafana.com/docs/grafana/latest/getting-started/)。

## 步骤一：获取Prometheus监控提供的专用API接口

该专用API接口是连接Prometheus和本地Grafana的纽带。请按照以下步骤获取该接口：

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  在**设置**页面顶部单击**Agent设置**。

5.  在**Agent设置**页签上，复制**步骤2：API接口地址**后的地址。

    ![pg_pm_settings_tab_agent_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4584298951/p103094.png)


## 步骤二：在本地Grafana添加数据源

将[步骤一](#section_1i3_18o_66s)获得的API接口地址添加为本地Grafana的数据源即可实现目标。请按照以下步骤添加数据源：

1.  以管理员账号登录本地Grafana系统。

2.  在左侧导航栏中选择**Configuration** \> **Data Sources**。

    **说明：** 仅管理员可以看到此菜单。

3.  在**Data Sources**页签上单击**Add data source**。

4.  在**Add data source**页面上单击**Prometheus**。

5.  在**Settings**页签的**Name**字段输入自定义的名称，在**URL**字段粘贴步骤一获得的API接口地址，并单击页签底部的**Save & Test**。

    ![tab_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2584298951/p103095.png)


## 验证结果

请按照以下步骤验证操作是否成功：

1.  登录本地Grafana系统。

2.  在左侧导航栏中单击**Explore**。

3.  在**Explore**页面顶部的下拉框中选择[步骤二](#section_c98_ybh_a8a)中添加的数据源，在**Metrics**字段输入指标名称并按回车。

    如果能显示出相应指标的图表，则说明操作成功。否则请检查填写的接口地址是否正确，以及数据源是否有Prometheus监控数据。

    ![pg_explore_with_metrics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2584298951/p103096.png)


