# View Grafana dashboards

On the Dashboards page of a Kubernetes cluster, you can view all Grafana dashboards of the Kubernetes cluster and the core metrics displayed on the dashboards. You can also update Grafana dashboards as required.

The Kubernetes cluster is monitored by Prometheus Service. For more information, see [Access to Alibaba Cloud Prometheus Service]().

## Go to a Grafana dashboard

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the monitored Kubernetes cluster resides. Then, click the name of the Kubernetes cluster in the K8s column.

    The **Dashboards** page displays the information about all Grafana dashboards of the Kubernetes cluster, including the dashboard name, dashboard version, dashboard type, data source, tags, core metrics, and status.

    |Parameter|Description|
    |---------|-----------|
    |Version|The version of the Grafana dashboard. Prometheus Service updates basic Grafana dashboards on an irregular basis.|
    |Type|The type of the Grafana dashboard. Valid values:    -   Basic: indicates a preset Grafana dashboard provided by Prometheus Service.
    -   Custom: indicates a custom Grafana dashboard. For more information, see [Use Prometheus Service to customize a Grafana dashboard](). |
    |Source|The source of the monitoring data in the Grafana dashboard.|
    |Tag|The tags of the monitored objects.|
    |Core Metric|The core metrics that are displayed on the Grafana dashboard.|
    |Status|The status of the Grafana dashboard.|


## Features

On the **Dashboards** page, you can perform the following operations:

-   View metrics

    Click the name of a Grafana dashboard. On the page that appears, you can view the real-time metrics on the Grafana dashboard. For more information about the metrics on basic dashboards, see [Basic metrics]().

-   View core metrics

    Find a Grafana dashboard that you want to view and move the pointer over the icon in the Core Metrics column. Then, the information about the core metrics is displayed. Click **Details**. The Details message appears. In the Details message, you can view the type and description of the core metrics.

-   Update a basic dashboard

    Find a Grafana dashboard whose name is suffixed with the **New** icon, and click **Upgrade** in the Actions column. In the message that appears, click **Upgrade**.

-   Reset basic dashboards

    On the **Dashboards** page, click **Reset Dashboard** in the upper-right corner. In the message that appears, click **Confirm**. Then, all basic dashboards are updated to the latest version.


**Related topics**  


[What is Prometheus Service?]()

