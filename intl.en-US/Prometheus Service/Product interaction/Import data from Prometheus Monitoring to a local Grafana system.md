---
keyword: [Prometheus, Grafana, local]
---

# Import data from Prometheus Monitoring to a local Grafana system

You can use the dedicated API provided by Prometheus Monitoring to view the monitoring data in a local Grafana system. This topic describes how to import data from Prometheus Monitoring to a local Grafana system.

-   The Prometheus agent is installed. For more information, see [Get started with Prometheus Service]().
-   Grafana is installed on a local host. For more information, see [Grafana](https://grafana.com/docs/grafana/latest/getting-started/what-is-grafana/).

## Step 1: Obtain the dedicated API provided by Prometheus Monitoring

The dedicated API connects Prometheus Monitoring to the local Grafana system. Perform the following steps to obtain the API:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the Container Service for Kubernetes cluster resides. Find the cluster and click **Settings** in the **Actions** column.

4.  On the **Settings** page, click the **Agent Settings** tab.

5.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.

    ![pg_pm_settings_tab_agent_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2714672161/p103094.png)


## Step 2: Add a data source to the local Grafana system

To add the API obtained in [Step 1](#section_1i3_18o_66s) as the data source of the local Grafana system, perform the following steps:

1.  Log on to the local Grafana system as the administrator.

2.  In the left-side navigation pane, choose **Configuration** \> **Data Sources**.

    **Note:** This menu is visible only to the administrator.

3.  On the **Data Sources** tab, click **Add Data Source**.

4.  On the **Add Data Source** page, click **Prometheus**.

5.  On the **Settings** tab, enter a name in the **Name** field, enter the API URL obtained in Step 1 in the **URL** field, and then click **Save & Test**.

    ![tab_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2714672161/p103095.png)


## Check the result

Perform the following steps to check whether the data source is added:

1.  Log on to the local Grafana system.

2.  In the left-side navigation pane, click **Explore**.

3.  Select the data source added in [Step 2](#section_c98_ybh_a8a) at the top of the **Explore** page, enter a metric name in the **Metrics** field, and then press the Enter key.

    If a chart of the metric is displayed, the data source is added. Otherwise, check whether the URL that you entered is correct and whether the data source contains the data from Prometheus Monitoring.

    ![pg_explore_with_metrics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2714672161/p103096.png)


