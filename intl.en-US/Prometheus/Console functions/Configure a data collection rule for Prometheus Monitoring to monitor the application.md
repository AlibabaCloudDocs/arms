# Configure a data collection rule for Prometheus Monitoring to monitor the application

You can edit the prometheus.yaml file or add ServiceMonitor to configure the data collection rule for Prometheus Monitoring to monitor an application.

The Prometheus agent has been installed for the application. For more information, see [Get started with Prometheus Service]().

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  Find the target cluster, and click**Settings** in the **Actions** column.

4.  You can configure the data collection rule for Prometheus Monitoring to monitor the application in the following scenarios:

    -   To monitor the business data of applications deployed in the Kubernetes cluster, such as order information, you can click **Add ServiceMonitor** on the **Details** tab. In the **Add ServiceMonitor** dialog box, enter the following information:

        ```
        apiVersion: monitoring.coreos.com/v1
        kind: ServiceMonitor
        metadata:
          # Enter a unique name.
          name: tomcat-demo
          # Enter the target namespace.
          namespace: default
        spec:
          endpoints:
          - interval: 30s
            # Enter the value of the Name field for Port of Prometheus Exporter.
            port: tomcat-monitor
            # Enter the value of the Path field for Prometheus Exporter.
            path: /prometheus-metrics
          namespaceSelector:
            any: true
          selector:
            matchLabels:
              # Enter the label field of service.yaml to locate the target service.yaml file.
              app: tomcat
        ```

    -   To monitor business data outside the Kubernetes cluster, such as the number of Redis connections, you can click **Edit prometheus.yaml** on the **Details** tab to configure the native prometheus.yaml file. In the **Edit prometheus.yaml** dialog box, enter the following information:

        ```
        global:
          scrape_interval:     15s
          evaluation_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
            - targets: ['localhost:9090']
        ```


