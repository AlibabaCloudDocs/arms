# Configure a data collection rule for Prometheus Monitoring to monitor the application

You can edit the prometheus.yaml file or add ServiceMonitor to configure the data collection rule for Prometheus Monitoring to monitor an application.

The Prometheus agent has been installed for the application. For more information, see [Get started with Prometheus Service]().

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  Find the target cluster, and click**Settings** in the **Actions** column.

4.  Configure data collection rules for ARMS Prometheus Monitoring to monitor the application in the following scenarios:

    -   To monitor the business data of the application deployed in the cluster, such as order information, you can click **Add ServiceMonitor** on the **Service Discovery** tab. In the **Add ServiceMonitor** dialog box, reference the following content to enter the text and click **OK**:

        ```
        apiVersion: monitoring.coreos.com/v1
        kind: ServiceMonitor
        metadata:
          #  Enter a unique name.
          name: tomcat-demo
          #  Enter a namespace.
          namespace: default
        spec:
          endpoints:
          - interval: 30s
            #  Enter the value of the Name field for Port of Prometheus Exporter in the service.yaml file.
            port: tomcat-monitor
            #  Enter the value of the Path field for Prometheus Exporter.
            path: /metrics
          namespaceSelector:
            any: true
            #  The namespace of Demo.
          selector:
            matchLabels:
              # Enter the value of the Label field in the service.yaml file to find the service.yaml file.
              app: tomcat
        ```

    -   To monitor business data outside the cluster, such as the number of Redis connections, you can reference the following content to enter the text on the **Prometheus Settings** tab and click **Save**:

        ```
        global:
          scrape_interval:     15s
          evaluation_interval: 15s
        scrape_configs:
          - job_name: 'prometheus'
            static_configs:
            - targets: ['localhost:9090']
        ```


