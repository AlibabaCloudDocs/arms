# Connect an ACK cluster to Prometheus Service

This topic describes how to connect a Container Service for Kubernetes \(ACK\) cluster to Prometheus Service. Then, you can use preset dashboards to monitor multiple performance metrics of hosts and the ACK cluster.

-   An ACK cluster is created. For more information, see [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md).
-   Application Real-Time Monitoring Service \(ARMS\) is activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick Start/Activate and upgrade ARMS.md).

## Enable ARMS Prometheus

You can enable ARMS Prometheus by using the following methods:

**Configure cluster parameters.**

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  In the upper-right corner of the Clusters page, click **Create Kubernetes Cluster**.

4.  Select the cluster template that you want to use and configure parameters for the new cluster. On the **Component Configurations**page, select **Enable Prometheus Monitoring**.

    For more information about how to create a cluster, see [Create a managed Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster/Create Kubernetes clusters/Create a managed Kubernetes cluster.md).

    **Note:** By default, **Enable Prometheus Monitoring** is selected when you create a cluster.

    After the cluster is created, the system automatically configures ARMS Prometheus.


**Enable ARMS Prometheus on the Prometheus Monitoring page in the ACK console.**

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, find the cluster that you want to manage and click the name of the cluster or click **Details** in the **Actions** column. The details page of the cluster appears.

4.  In the left-side navigation pane of the cluster management page, choose **Operations** \> **Prometheus Monitoring**.

5.  In the middle of the **Prometheus Monitoring** page, click **Install**.


**Enable the feature on the App Catalog page in the ACK console.**

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Marketplace** \> **App Catalog**.

3.  On the App Catalog page, click the **Alibaba Cloud Apps** tab and click **ack-arms-prometheus**.

4.  On the App Catalog - ack-arms-prometheus page, click the **Parameters** tab.

5.  On the **Parameters** tab, set parameter cluster\_id.

    **Note:**

    The system automatically sets the value to the ID of the cluster that you create. You can perform the following steps to view the cluster ID: In the left-side navigation pane of the ACK console, choose **Clusters** \> **Clusters**. On the page that appears, the cluster ID is displayed below each cluster name.

6.  In the **Deploy** section of the App Catalog - ack-arms-prometheus page, select the cluster for which you want to enable ARMS Prometheus, and click **Create**.

    **Note:** By default, **Namespace** and **Release Name** are set to **arms-prom**.


## Go to a Grafana dashboard

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the ACK cluster resides. Then, click the dashboard that you want to view in the **Installed Dashboards** column.


## Uninstall the Prometheus agent

To disable Prometheus monitoring for the ACK cluster, perform the following steps to uninstall the Prometheus agent:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the ACK cluster resides. Then, find the ACK cluster and click **Uninstall** in the **Actions** column.

4.  In the **Confirmation** message, click **OK**.

    After you uninstall the Prometheus agent, the dashboards of the ACK cluster disappear from the **Installed Dashboards** column.

5.  Log on to the [ACK console](https://cs.console.aliyun.com).

6.  In the left-side navigation pane, click **Clusters**. On the Clusters page, find the cluster for which you want to disable Prometheus monitoring and click its name.

7.  In the left-side navigation pane, choose **Applications** \> **Helm**. Perform one of the following operations as needed:

    -   If no record in the `arms-prom-****` format is displayed on the **Helm** page, the Prometheus agent is uninstalled. In this case, you do not need to perform other operations.
    -   If a record in the `arms-prom-****` format is displayed on the **Helm** page, click **Delete** in the **Actions** column.

        ![ack_pg_release](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8165893161/p143010.png)


