---
keyword: [Prometheus, Grafana, local]
---

# Import monitoring data from Prometheus Service to a local Grafana system

You can use the dedicated API provided by Prometheus Service to view the monitoring data in a local Grafana system. This topic describes how to import monitoring data from Prometheus Service to a local Grafana system.

-   The Prometheus agent is installed. For more information, see [Get started with Prometheus Service]().
-   Grafana is installed on a local host. For more information, see [Grafana](https://grafana.com/docs/grafana/latest/getting-started/what-is-grafana/).

## Step 1: Obtain the dedicated API of Prometheus Service

This dedicated API connects Prometheus Service and the local Grafana system. Perform the following steps to obtain the API:

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the Container Service for Kubernetes cluster resides. Find the cluster and click **Settings** in the **Actions** column.

3.  On the **Settings** page, click the **Agent Settings** tab.

4.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.


## Step 2: Add a data source to the local Grafana system

To add the API obtained in [Step 1](#section_1i3_18o_66s) as the data source of the local Grafana system, perform the following steps:

1.  Log on to the local Grafana system as the administrator.

2.  In the left-side navigation pane, choose **Configuration** \> **Data Sources**.

    **Note:** Only the administrator can view this menu.

3.  On the **Data Sources** tab, click **Add Data Source**.

4.  On the **Add Data Source** page, click **Prometheus**.


## Check the result

Perform the following steps to check whether the data source is added:

1.  Log on to the local Grafana system.

2.  In the left-side navigation pane, click **Explore**.

3.  Select the data source added in [Step 2](#section_c98_ybh_a8a) on the top of the **Explore** page, enter the metric name in the **Metrics** field, and then press Enter.

    If a chart of the corresponding metric is displayed, the operation is successful. Otherwise, check whether the URL you entered is correct, and whether the data source contains the monitoring data of Prometheus Service.


