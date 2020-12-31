# What is Prometheus Service?

Prometheus Service is a managed monitoring service that is provided by Alibaba Cloud. Prometheus Service is compatible with the open source Prometheus ecosystem. Prometheus Service monitors a wide variety of components and provides various ready-to-use dashboards.

## Introduction to Prometheus

Prometheus is an open source system monitoring and alerting framework. It is inspired by the Borgmon monitoring system of Google. In 2012, SoundCloud employees who had worked for Google created Prometheus and developed it as an open source and community-driven project. In 2015, the project was officially released. In 2016, Prometheus joined the [Cloud Native Computing Foundation \(CNCF\)](https://cncf.io/) and became a project second only to Kubernetes in popularity.

Prometheus has the following features:

-   Implements a multi-dimensional data model \(key-value pairs based on time series\)
-   Provides a flexible query and aggregation language called Prometheus Query Language \(PromQL\)
-   Provides local and distributed storage
-   Collects time series data by using the HTTP Pull model
-   Implements the HTTP Push model by using an intermediary service named Pushgateway
-   Discovers scrape targets by using the file-based service discovery mechanism or static configuration
-   Supports various charts and dashboards

## Advantages of Alibaba Cloud Prometheus Service over open source Prometheus

Compared with the open source Prometheus, Alibaba Cloud Prometheus Service has the following advantages:

-   Lightweight deployment, stability, and accuracy
-   Unlimited data collection and storage
-   Compatibility with open source Prometheus
-   Cost-effectiveness

## Lightweight deployment, stability, and accuracy

-   Compared with the open source Prometheus, the deployment of Alibaba Cloud Prometheus Service is more lightweight. Instead of building a Prometheus monitoring system, you can install the Prometheus agent \(PromAgent\) to monitor your business.

    ![dg_arms_prometheus_advantage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735344851/p76745.png)

-   The open source Prometheus consumes 16 GB to 128 GB of memory. Alibaba Cloud Prometheus Service consumes only 200 MB to 1 GB of memory and 1 CPU core. Alibaba Cloud Prometheus Service provides higher system stability than the open source Prometheus.
-   The open source Prometheus retrieves data only once, and data may be discarded when it is written to the storage component. Alibaba Cloud Prometheus Service retries multiple times if it fails to retrieve data. It ensures high concurrency when it writes data to the storage component. No data is discarded.

## Unlimited data collection and storage

-   The open source Prometheus can collect data based on up to one million metrics. Alibaba Cloud Prometheus Service can scale its data collection capability based on the number of Kubernetes replicas. Collection tasks can be distributed across replicas.
-   The maximum storage capacity of the open source Prometheus is limited by the size of the local disk. Alibaba Cloud Prometheus Service uses the central cloud storage service. The storage capacity is not limited.

## Compatibility with open source Prometheus

-   Alibaba Cloud Prometheus Service is compatible with the clients and query languages in the open source Prometheus ecosystem. Alibaba Cloud Prometheus Service provides optimized collection rules and usage values.

    ![dg_arms_prometheus_ecology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6735344851/p76971.png)

-   Alibaba Cloud Prometheus Service is compatible with three mainstream collection rules: the open source prometheus.yaml configuration file, ServiceMonitor, and the default collection rule named Annotation. ServiceMonitor is suitable for the monitoring of custom Kubernetes clusters. Compared with the open source Prometheus, Alibaba Cloud Prometheus Service allows you to update collection rules by using the prometheus.yaml configuration file. You do not need to write multiple lines of code in the Deployment file. You only need to add the following three Annotations.

    ```
    prometheus.io/scrape: "true"
    prometheus.io/port: "9090"
    prometheus.io/path: "/metrics"
    ```

-   Alibaba Cloud Prometheus Service allows you to visualize data by using Grafana. By configuring the Prometheus HTTP API URL, you can implement multi-tenant isolation for the data source in Grafana and multi-tenant isolation for the Grafana dashboard. Alibaba Cloud Prometheus Service is also compatible with the Explore data debugging module of Grafana.
-   Alibaba Cloud Prometheus Service is compatible with the HTTP API module of the open source Prometheus. It supports three standard API operations: query, query\_range, and labelValues. In addition, you can add /userId/clusterId/regionId/ to the data URL to achieve multi-tenant isolation.
-   Alibaba Cloud Prometheus Service uses the built-in alerting system of Application Real-Time Monitoring Service \(ARMS\) and is compatible with the alert rules of the open source Prometheus.

## Cost-effectiveness

-   Alibaba Cloud Prometheus Service supports the default Kubernetes monitoring. After you install the default Kubernetes monitoring, Alibaba Cloud Prometheus Service automatically creates exporters, collection rules, Grafana dashboards, and ARMS alerts. Compared with the open source Prometheus, Alibaba Cloud Prometheus Service reduces your time cost from about 3 days to about 10 minutes.

    ![Dashboard 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8885468061/p103080.png)

-   Alibaba Cloud Prometheus Service supports the monitoring of open source components. You only need to enter the AccessKey ID and AccessKey secret of your Alibaba Cloud account, and the accounts and passwords of the RDS and Redis components. Alibaba Cloud Prometheus Service creates exporters and dashboards for these components. Compared with the open source Prometheus, Alibaba Cloud Prometheus Service reduces your time cost from about 7 days to about 3 minutes.

    ![Dashboard 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8885468061/p103081.png)

-   Alibaba Cloud Prometheus Service supports easy installation and removal. You can debug the service by performing health checks. Compared with the open source Prometheus, Alibaba Cloud Prometheus Service reduces your time cost from about 1 day to about 3 minutes.

