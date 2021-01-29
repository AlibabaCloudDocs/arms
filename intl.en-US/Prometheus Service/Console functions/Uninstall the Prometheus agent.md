# Uninstall the Prometheus agent

To disable Prometheus Monitoring for a Kubernetes cluster, you can perform the following operations to uninstall the Prometheus agent:

## Procedure

1.  Log on to the [ARMS console](https://arms.console.aliyun.com/#/home)[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the **Prometheus Monitoring** page, select a region in the upper-left corner and click **Uninstall** in the **Actions** column. In the **Confirmation** message, click **OK**.

    After you uninstall the agent, no dashboard is displayed in the **Installed Dashboards** column. Then, you must go to the Container Service for Kubernetes console to check whether the uninstallation is successful.

4.  Log on to the [ACK console](https://cs.console.aliyun.com)[ACK console](https://partners-intl.console.aliyun.com/#/cs).

5.  In the left-side navigation pane, click **Clusters**. On the Clusters page, find the cluster for which you want to disable Prometheus Monitoring and click its name.

    **Note:** The operations described in this topic are applicable only to the new version of the Container Service for Kubernetes console. If you are using the earlier version of the console, choose **Clusters** \> **Clusters** in the left-side navigation pane and click **New Version** in the upper-right corner of the page.

6.  In the left-side navigation pane, click **Helm**. Perform one of the following operations based on the scenario:

    -   If no `arms-prom-****` record is displayed on the **Helm** page, the monitoring agent is uninstalled. You do not need to perform other operations.
    -   If the `arms-prom-****` record is displayed on the **Helm** page, click **Delete** in the **Actions** column.

        ![ack_pg_release](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5709088061/p143010.png)


