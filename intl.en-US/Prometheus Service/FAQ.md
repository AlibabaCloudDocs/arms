---
keyword: [Prometheus Service, FAQ, integration]
---

# FAQ

This topic provides answers to some frequently asked questions about Prometheus Service.

## Overview

-   [How can I prevent Prometheus Service from automatically creating default alert rules?](#section_7bu_xio_mii)
-   [How can I allow Prometheus Service to automatically enable alert rules?](#section_vsq_o9l_nyk)
-   [How can I integrate Prometheus Service with third-party systems such as Grafana, Istio, and HPA?](#section_zb5_wdo_ofw)
-   [What can I do if the Prometheus agent is not deleted after the monitored ACK cluster is deleted?](#section_7v0_4pa_yom)

## How can I prevent Prometheus Service from automatically creating default alert rules?

Prometheus Service automatically creates default alert rules for monitored applications. For more information about the default alert rules, see [Description of alert rules]().

Prometheus Service provides the defaultAlert parameter that allows you to control whether Prometheus Service automatically creates default alert rules. If this parameter is set to true, Prometheus Service automatically creates default alert rules. If this parameter is set to false, Prometheus Service does not automatically create default alert rules.

To prevent Prometheus Service from automatically creating default alert rules for a monitored application, you can set the defaultAlert parameter of the Prometheus agent to false. After you disable automatic creation of default alert rules, we recommend that you delete the default alert rules that have been created by Prometheus Service for your application.

The following example shows how to configure the Prometheus agent for a Container Service for Kubernetes \(ACK\) cluster.

1.  Set the defaultAlert parameter of the Prometheus agent to false.

    1.  Log on to the [ACK console](https://cs.console.aliyun.com).

    2.  In the left-side navigation pane, click **Clusters**.

    3.  On the Clusters page, find the cluster that you want to manage and click **Applications** in the **Actions** column.

    4.  On the **Deployments** page, set **Namespace** to arms-prom, find the deployment whose name starts with arms-prom, such as arms-prom-ack-arms-prometheus, and then click **Edit** in the **Actions** column.

    5.  On the **Edit** page, find the **Start** parameter in the **Lifecycle** section. In the **Parameter** field, add -defaultAlert=false. Then, click **Update** in the upper-right corner of the page.

        After the Prometheus agent is updated, wait 3 to 5 minutes. Prometheus Service no longer creates default alert rules for the cluster.

2.  Delete default alert rules.

    1.  Log on to the [Application Real-Time Monitoring Service \(ARMS\) console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

    2.  In the left-side navigation pane, click **Prometheus Monitoring**.

    3.  On the Prometheus Monitoring page, click the name of the ACK cluster that you want to manage.

    4.  In the left-side navigation pane, click **Settings**.

    5.  On the page that appears, click the **Rule** tab and delete the alert rules.

        ![Rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7168355161/p248872.png)


## How can I allow Prometheus Service to automatically enable alert rules?

By default, alert rules are disabled.

Prometheus Service provides the alert parameter that allows you to control whether Prometheus Service automatically enables alert rules. If this parameter is set to true, Prometheus Service automatically enables alert rules. If this parameter is set to false, Prometheus Service does not automatically enable alert rules.

To allow Prometheus Service to automatically enable alert rules that are created for a monitored application, you can set the alert parameter of the Prometheus agent to true.

The following example shows how to configure the Prometheus agent for an ACK cluster.

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane of the ACK console, click **Clusters**.

3.  On the Clusters page, find the cluster that you want to manage and click **Applications** in the **Actions** column.

4.  On the **Deployments** page, set **Namespace** to arms-prom, find the deployment whose name starts with arms-prom, such as arms-prom-ack-arms-prometheus, and then click **Edit** in the **Actions** column.

5.  On the **Edit** page, find the **Start** parameter in the **Lifecycle** section. In the **Parameter** field, add -alert=true. Then, click **Update** in the upper-right corner of the page.

    After the Prometheus agent is updated, wait 3 to 5 minutes. All alert rules are enabled for the cluster.


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

After an ACK cluster is deleted, the following issues occur in the region where the deleted ACK cluster resides:

-   On the Prometheus Monitoring page of the [Prometheus Service console](https://prometheus.console.aliyun.com/#/home), several clusters are dimmed.
-   You cannot create an ACK cluster by using the name of the deleted ACK cluster.

**Solution**

Log on to the [Prometheus Service console](https://prometheus.console.aliyun.com/#/home) and uninstall the Prometheus agent. For more information, see [Uninstall the Prometheus agent]().

**Related topics**  


[Import data from Prometheus Monitoring to a local Grafana system]()

