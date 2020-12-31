# Get started with Prometheus Service

To monitor a Container Service for Kubernetes \(ACK\) cluster, you can install the Prometheus agent in the Application Real-Time Monitoring Service \(ARMS\) console. Then, you can monitor your hosts and ACK cluster on a predefined dashboard by using various performance metrics.

-   An ACK cluster is created. For more information, see [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md).
-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md)

## Enable ARMS Prometheus monitoring

You can enable ARMS Prometheus monitoring by using the following three methods:

**Configure cluster parameters.**

1.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  In the upper-right corner of the Clusters page, click **Create Kubernetes cluster**.

4.  Select the cluster template that you want to use and configure parameters for the new cluster. On the **Component Configurations**page, select **Enable Prometheus Monitoring**.

    For more information about how to create a cluster, see [Create a managed Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster management/Create Kubernetes clusters/Create a managed Kubernetes cluster.md).

    **Note:** By default, **Enable Prometheus Monitoring** is selected when you create a cluster.

    After the cluster is created, the system automatically configures ARMS Prometheus monitoring.


**Enable the feature on the Prometheus Monitoring page in the ACK console.**

1.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, find the cluster that you want to manage and click **Details** in the **Actions** column.

4.  In the left-side navigation pane of the cluster management page, choose **Operations** \> **Prometheus Monitoring**.

5.  In the middle of the **Prometheus Monitoring** page, click **Install**.


**Enable the feature on the App Catalog page in the ACK console.**

1.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Marketplace** \> **App Catalog**.

3.  On the App Catalog page, click the**Alibaba Cloud Apps** tab and click **ack-arms-prometheus**.

4.  On the App Catalog - ack-arms-prometheus page, click the **Parameters** tab.

5.  On the **Parameters** tab, set parameter cluster\_id.

    **Note:**

    The system automatically sets the value to the ID of the cluster that you create. You can perform the following steps to view the cluster ID: In the left-side navigation pane of the ACK console, choose **Clusters** \> **Clusters**. On the page that appears, the string below each cluster name is the cluster ID.

6.  In the **Deploy** section of the App Catalog - ack-arms-prometheus page, select the cluster for which you want to enable Prometheus monitoring, and click **Create**.

    **Note:** By default, **Namespace** and **Release Name** are set to **arms-prom**.


## Open a Prometheus dashboard

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner, select a region. Click a link in the **Installed Dashboards** column to open a monitoring dashboard in a new window.


## Uninstall the Prometheus agent

To disable Prometheus monitoring for the ACK cluster, perform the following steps to uninstall the Prometheus agent:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner, select a region. Click **Uninstall** in the **Actions** column. In the **Confirmation** dialog box, click **OK**.

    After you uninstall the agent, the dashboards are no longer displayed in the **Installed Dashboards** column. Go to the Container Service for Kubernetes console to check whether the uninstallation is successful.

4.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

5.  In the left-side navigation pane, click **Clusters**, and then click the name of the cluster for which you want to disable Prometheus monitoring.

    **Note:** The steps described in this topic are only applicable to the new version of the Container Service for Kubernetes console. If you are using the previous version, choose **Clusters** \> **Clusters** in the left-side navigation pane, then click **New version** in the upper-right corner of the page.

6.  In the left-side navigation pane, click **Releases**. Perform one of the following operations based on your needs:

    -   If the `arms-prom-***` record is not displayed on the **Releases** page, the Prometheus agent is uninstalled. You do not need to perform further operations.
    -   If the `arms-prom-***` record is displayed on the **Releases** page, click **Delete** in the **Actions** column.

        ![ack_pg_release](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5709088061/p143010.png)


**Related topics**  


[What is Prometheus Service?]()

