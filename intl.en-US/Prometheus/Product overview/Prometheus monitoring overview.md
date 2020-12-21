# Prometheus monitoring overview

ARMS Prometheus fully integrates with the open-source Prometheus ecosystem, supports monitoring by a wide range of components, provides a variety of pre-available monitoring dashboards, and provides fully managed Prometheus services.

## What is Prometheus?

Prometheus is an open-source system monitoring and alarm framework inspired by Google&\#39;s borgnon monitoring system. In 2012, former Google employees of SoundCloud created Prometheus and developed it as an open source project in the community. On 2015, the project was officially released. In 2016, Prometheus joined the Cloud Native Computing Foundation \([Cloud Native Computing Foundation](https://cncf.io/)\), Becoming a project second only to Kubernetes in popularity.

Prometheus has the following features:

-   Multi-Dimensional Data Model \(Key-Value pairs based on time series\)
-   Flexible query and aggregation language PromQL
-   Local and distributed storage
-   Collect time series data by using an HTTP push model
-   Pushgateway \(an optional Prometheus middleware\) can be used to implement the Push mode.
-   Discover target machines through dynamic service discovery or static configuration
-   Supports multiple charts and data dashboards.

## Advantages of ARMS Prometheus monitoring and open-source Prometheus monitoring

Overall, compared with open-source Prometheus monitoring, ARMS Prometheus monitoring has the following advantages:

-   More lightweight, more stable, and more accurate
-   Unlimited data volume
-   Fully compatible with the open-source ecosystem
-   Cost saving

## More lightweight, more stable, and more accurate

-   Compared with open-source Prometheus monitoring, the overall structure of ARMS Prometheus monitoring is more lightweight. You do not need to build your own Prometheus monitoring system. Instead, you only need to install ARMS Prometheus monitoring agent PromAgent to start monitoring services.

    ![Dg_arms_prometheus_frontage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735344851/p76745.png)

-   In terms of system stability, the open-source Prometheus monitoring generally occupies 16 GB ~ 128 GB memory, while ARMS Prometheus only uses 200 MB ~ 1 GB memory and 1 core CPU. Compared with open-source Prometheus monitoring, ARMS Prometheus monitoring is more stable.
-   In terms of the accuracy of data capturing and writing, the open-source Prometheus monitoring only captures data once, and the discarding logic exists when the data is written to the storage component instantly. However, ARMS Prometheus retries capturing data five times and continuously writes the data to the storage component concurrently without the discard logic.

## Unlimited data volume

-   The maximum data collection capability of the open-source Prometheus monitoring system is millions of Metrics. The data collection capability of the ARMS Prometheus monitoring system can be scaled based on the number of K8s replicas to break down collection tasks in a balanced manner.
-   The upper limit of data storage capability of the open-source Prometheus monitoring system is limited by the size of the local disk, while the storage capability of the central cloud storage service of ARMS Prometheus monitoring system is theoretically unlimited.

## Fully compatible with the open-source ecosystem

-   ARMS Prometheus is fully compatible with the clients and query languages in the open-source ecosystem of Prometheus, as well as the collection rules and usage value in the open-source ecosystem.

    ![Dg_arms_prometheus_ecovery](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735344851/p76971.png)

-   ARMS Prometheus monitoring is compatible with three mainstream collection rules, including standard open sourceprometheus.yamlCollection rule configuration file, collection rule ServiceMonitor suitable for custom K8s monitoring, and default collection rule Annotation. Compared with open-source Prometheus monitoring, ARMS Prometheus monitoring can be used without restarting.prometheus.yamlConfiguration files update collection rules dynamically. InDeploymentYou do not need to write multiple lines of code in the file. You only need to add the following three annotations:

    ```
    prometheus.io/scrape: &quot;true&quot;
    prometheus.io/port: &quot;9090&quot;
    prometheus.io/path: &quot;/metrics&quot;
    ```

-   ARMS Prometheus is compatible with Grafana. By configuring the Prometheus http api url, you can implement multi-tenant isolation of data sources and multi-tenant isolation of the Grafana dashboard in Grafana. ARMS Prometheus is also compatible with the Explore data debugging module of Grafana.
-   ARMS Prometheus is compatible with the http api module of open-source Prometheus monitoring. It supports three standard data query interfaces: query, query\_range, and labelValues. You can add/userId/clusterId/regionId/This group of IDs achieves multi-tenant isolation.
-   Although ARMS Prometheus monitoring uses the existing alerting system of ARMS, it is fully compatible with the alerting rule PromQL of open-source Prometheus monitoring.

## Cost saving

-   ARMS Prometheus supports K8s monitoring by default. After you install the default K8s monitoring, ARMS Prometheus automatically creates default reporter, collection rule, Grafana dashboard, and ARMS alarms for you. Your time cost can be reduced from about 3 days when you used open-source Prometheus to monitor K8s to about 10 minutes.

    ![Pg_prom_default_k8s_dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735344851/p77075.png)

-   ARMS Prometheus supports open-source component monitoring. You only need to enter the AccessKeyId and AccessKeySecret of your Alibaba Cloud account, as well as the account and password for the RDS and Redis components. ARMS Prometheus automatically generates an Exporter for these components by default. and create a default widget dashboard. Your time cost can be reduced from about 7 days when you used open source Prometheus to monitor open source components to about 3 minutes.

    ![Pg_prom_mysql_dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7735344851/p77072.png)

-   ARMS Prometheus supports one-click installation, one-click removal, and debugging of Prometheus monitoring through health check. Your time cost can be reduced from about one day when you used open-source Prometheus monitoring to about three minutes.

