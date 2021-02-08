# 配置Prometheus监控采集规则

您可以通过编辑prometheus.yaml或添加ServiceMonitor的方式为应用配置Prometheus监控的采集规则。

已成功为应用安装Prometheus监控插件，详情请参见[开始使用Prometheus监控]()。

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在**Prometheus监控**页面左上角选择容器服务K8s集群所在的地域，并在目标集群右侧的**操作**列单击**设置**。

4.  为应用配置Prometheus监控采集规则分为以下两种情况。

    -   如果您需要监控部署在K8s集群内的应用的业务数据，例如订单信息，可以在**服务发现**页签上单击**添加ServiceMonitor**，并在**添加ServiceMonitor**对话框中参考以下示例内容进行填写，然后单击**确定**。

        ```
        apiVersion: monitoring.coreos.com/v1
        kind: ServiceMonitor
        metadata:
          #  填写一个唯一名称
          name: tomcat-demo
          #  填写目标命名空间
          namespace: default
        spec:
          endpoints:
          - interval: 30s
            #  填写service.yaml中Prometheus Exporter对应的Port的Name字段的值
            port: tomcat-monitor
            #  填写Prometheus Exporter对应的Path的值
            path: /metrics
          namespaceSelector:
            any: true
            #  Demo的命名空间
          selector:
            matchLabels:
              #  填写service.yaml的Label字段的值以定位目标service.yaml
              app: tomcat
        ```

    -   如果您需要监控部署在K8s集群之外的业务数据，如Redis连接数时，可以在**Prometheus设置**页签上参考以下示例内容进行填写，然后单击**保存**。

        ```
        global:
          scrape_interval:     15s
          evaluation_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
            - targets: ['localhost:9090']
        ```


