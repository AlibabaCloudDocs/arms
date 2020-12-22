---
keyword: [Prometheus, Grafana, local]
---

# Import ARMS Prometheus Monitoring data to local Grafana

You can use the dedicated API provided by Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring to view the ARMS Prometheus Monitoring data in local Grafana. This topic describes how to import ARMS Prometheus Monitoring data to local Grafana.

-   You have installed the ARMS Prometheus Monitoring agent. For more information, see [Get started with Prometheus Service]().
-   You have installed Grafana locally. For more information, see [Grafana](https://grafana.com/docs/grafana/latest/getting-started/what-is-grafana/).

## Quick start

## Step 1: Obtain the dedicated API provided by ARMS Prometheus Monitoring

This dedicated API connects ARMS Prometheus Monitoring and local Grafana. Perform the following steps to obtain the API:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**. On the **Prometheus Monitoring** page, select the target region on the top and click **Settings** in the **Actions** column of the target Kubernetes cluster.

3.  On the **Settings** page, click the **Agent Settings** tab.

4.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.

    ![pg_pm_settings_tab_agent_settings](../images/p103094.png)


## Step 2: Add a data source to the local Grafana

Perform the following steps to add the API obtained in [Step 1](#section_1i3_18o_66s) as the data source of local Grafana:

1.  Log on to the local Grafana system as the administrator.

2.  In the left-side navigation pane, choose **Configuration** \> **Data Sources**.

    **Note:** Only the administrator can view this menu.

3.  On the **Data Sources** tab, click **Add Data Source**.

4.  On the **Add Data Source** page, click **Prometheus**.

5.  On the **Settings** tab, set **Name** to the custom name, enter the API obtained in Step 1 in the **URL** field, and then click **Save & Test**.

    ![tab_settings](../images/p103095.png)


## Verification

Perform the following steps to check whether the data source is added:

1.  Log on to the local Grafana system.

2.  In the left-side navigation pane, click **Explore**.

3.  Select the data source added in [Step 2](#section_c98_ybh_a8a) on the top of the **Explore** page, enter the metric name in the **Metrics** field, and then press Enter.

    If a chart of the corresponding metric is displayed, the operation is successful. Otherwise, check whether the URL you entered is correct, and whether the data source contains ARMS Prometheus Monitoring data.

    ![pg_explore_with_metrics](../images/p103096.png)


