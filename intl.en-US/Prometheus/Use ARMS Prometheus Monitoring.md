# Use ARMS Prometheus Monitoring

For Container Service Kubernetes clusters, you can install the Prometheus agent in Application Real-Time Monitoring Service \(ARMS\) with one click. Then, you can monitor multiple performance metrics of hosts and Kubernetes clusters through the predefined dashboards.

## Prerequisites

-   [Create a managed Kubernetes cluster](/intl.en-US/Quick Start/Basic operations/Create a managed Kubernetes cluster.md): Create a Container Service Kubernetes cluster.
-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md)

## Install the Prometheus agent

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Prometheus Monitoring**.

    On the Prometheus monitoring page, all the Container Service Kubernetes clusters under your Alibaba Cloud account are displayed.

3.  On the Prometheus monitoring page, click **Installation** in the **Actions** column. In the Tips dialog box, click **OK**.

    During agent installation, the installation progress is displayed by a progress bar and is also displayed as a percentage in the **Actions** column.

    After the Prometheus agent is installed, all installed agents are displayed in the **Has installation plugins** column.

    **Note:** If the installation fails, retry until it is successful. If the installation still fails after several attempts, contact us at our DingTalk account `23148410`.


## Access Prometheus dashboards

1.  In the left-side navigation pane, click **Prometheus Monitoring**.

2.  On the Prometheus monitoring page, click a link in the **Has installation plugins** column to access the monitoring dashboard in a new browser window.


## Uninstall the Prometheus agent

To disable Prometheus Monitoring for a Kubernetes cluster, uninstall the Prometheus agent as follows:

1.  In the left-side navigation pane, click **Prometheus Monitoring**.

2.  On the Prometheus monitoring page, click **Unloading** in the **Actions** column. In the Tips dialog box, click **OK**.

    After the agent is uninstalled, the agent is no longer displayed in the **Has installation plugins** column.


## Next steps

[View the metrics of Prometheus Service]()

## More information

[What is Prometheus Service?]()

