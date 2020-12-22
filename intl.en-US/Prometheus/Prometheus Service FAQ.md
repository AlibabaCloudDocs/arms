---
keyword: [Prometheus Service, FAQ, integration]
---

# Prometheus Service FAQ

This topic provides answers to some commonly asked questions about Prometheus Service.

## How can I integrate Prometheus Service with third-party systems such as Grafana, Istio, and HPA?

To integrate Prometheus Service with third-party systems such as Grafana, Istio, and Horizontal Pod Autoscaler \(HPA\), you must obtain the API URL of Prometheus Service. Perform the following steps to obtain the API URL:

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner of the **Prometheus Monitoring** page, select the region where the Container Service for Kubernetes cluster resides. Find the cluster and click **Settings** in the **Actions** column.

3.  On the **Settings** page, click the **Agent Settings** tab.

4.  On the **Agent Settings** tab, copy the URL next to **Step 2: API URL**.


After you obtain the API URL, add it to third-party systems such as Grafana, Istio, and HPA. For more information about how to integrate Prometheus Service with Grafana, see [Import monitoring data from Prometheus Service to a local Grafana system]().

**Related topics**  


[Import monitoring data from Prometheus Service to a local Grafana system]()

