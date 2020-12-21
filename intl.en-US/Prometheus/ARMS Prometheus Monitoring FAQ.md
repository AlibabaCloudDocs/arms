---
keyword: [Prometheus Monitoring, FAQ, integration]
---

# ARMS Prometheus Monitoring FAQ

This topic summarizes the FAQ about using Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring.

## How is ARMS Prometheus Monitoring integrated into third-party systems such as Grafana, Istio, and HPA?

To integrate Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring into third-party systems such as Grafana, Istio, and Horizontal Pod Autoscaler \(HPA\), you must obtain the API URL of ARMS Prometheus Monitoring. Perform the following steps to obtain the API URL:

1.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the Container Service for Kubernetes cluster resides. Find the cluster and click **Settings** in the **Actions** column.

2.  On the **Settings** page, click the **Agent Settings** tab.

3.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.

    ![pg_pm_settings_tab_agent_settings](../images/p103094.png)


After you obtain the API URL, add it to the third-party systems such as Grafana, Istio, and HPA. For more information about how to integrate ARMS Prometheus Monitoring into Grafana, see [Import monitoring data from Prometheus Service to a local Grafana system]().

**Related topics**  


[Import monitoring data from Prometheus Service to a local Grafana system]()

