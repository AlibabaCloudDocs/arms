---
keyword: [Prometheus Service, FAQ, integration]
---

# Prometheus Service FAQ

This topic provides answers to some frequently asked questions about Prometheus Service.

## Overview

-   [How can I integrate Prometheus Service with third-party systems such as Grafana, Istio, and HPA?](#section_zb5_wdo_ofw)
-   [What can I do if the Prometheus agent is not deleted after the monitored ACK cluster is deleted?](#section_7v0_4pa_yom)

## How can I integrate Prometheus Service with third-party systems such as Grafana, Istio, and HPA?

To integrate Prometheus Service with third-party systems such as Grafana, Istio, and Horizontal Pod Autoscaler \(HPA\), you must obtain the API URL of Prometheus Service. Perform the following steps to obtain the API URL:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the Container Service for Kubernetes cluster resides. Find the cluster and click **Settings** in the **Actions** column.

4.  On the **Settings** page, click the **Agent Settings** tab.

5.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.

    ![pg_pm_settings_tab_agent_settings](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2714672161/p103094.png)


After you obtain the API URL, add it to third-party systems such as Grafana, Istio, and HPA. For more information about how to integrate Prometheus Service with Grafana, see [Import data from Prometheus Monitoring to a local Grafana system]().

## What can I do if the Prometheus agent is not deleted after the monitored ACK cluster is deleted?

**Problem description**

After a Container Service for Kubernetes \(ACK\) cluster is deleted, the following issues occur in the region where the deleted ACK cluster resides:

-   On the Prometheus Monitoring page of the [Prometheus Service console](https://prometheus.console.aliyun.com/#/home), several clusters are dimmed.
-   You cannot create an ACK cluster by using the name of the deleted ACK cluster.

**Solution**

Log on to the [Prometheus Service console](https://prometheus.console.aliyun.com/#/home) and uninstall the Prometheus agent. For more information, see [Uninstall the Prometheus agent]().

**Related topics**  


[Import data from Prometheus Monitoring to a local Grafana system]()

