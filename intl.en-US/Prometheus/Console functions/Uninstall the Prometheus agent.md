# Uninstall the Prometheus agent

To disable Prometheus monitoring for a Kubernetes cluster, you can perform the following steps to uninstall the Prometheus agent.

## Procedure

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  On the **Prometheus Monitoring** page, select a region in the upper-left corner, and then click **Uninstall** in the **Actions** column. In the **Confirmation** dialog box, click **OK**.

    After you uninstall the agent, no dashboard is displayed in the **Installed Dashboards** column. Then, you must go to the Container Service for Kubernetes \(ACK\) console to check whether the uninstallation is successful.

3.  Log on to the [ACK console](https://cs.console.aliyun.com).

4.  In the left-side navigation pane, click **Clusters**, and then click the name of the cluster that you want to stop monitoring.

    **Note:** The steps described in this topic in the Container Service console are applicable only to the new version of the console. If you are using the earlier version of the console, choose **Clusters** \> **Clusters** in the left-side navigation pane, and then click **New Version** in the upper-right corner of the page.

5.  In the left-side navigation pane, click **Releases**, and then perform the following operations as needed:

    -   If no `arms-prom-****` record is displayed on the **Releases** page, the monitoring agent is uninstalled. You do not need to perform other operations.
    -   If the `arms-prom-****` record is displayed on the **Releases** page, click **Delete** in the **Actions** column.

