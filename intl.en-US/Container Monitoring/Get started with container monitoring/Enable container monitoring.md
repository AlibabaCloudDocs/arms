# Enable container monitoring

The public preview of container monitoring starts from June 18, 2021. During the public preview, you can use this feature for free. If you have questions, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help. This topic shows you how to install related components to enable container monitoring.

-   Application Real-Time Monitoring Service \(ARMS\) is activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick Start/Activate and upgrade ARMS.md).
-   A Kubernetes cluster is created in the Container Service for Kubernetes \(ACK\) console. For more information, see [Create a dedicated Kubernetes cluster](/intl.en-US/User Guide for Kubernetes Clusters/Cluster/Create Kubernetes clusters/Create a dedicated Kubernetes cluster.md).

## Enable container monitoring in the ACK console

1.  Install the component for Prometheus monitoring, ack-arms-prometheus.

    1.  Log on to the [ACK console](https://cs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Marketplace** \> **App Catalog**.

    3.  On the App Catalog page, find and click **ack-arms-prometheus**.

    4.  On the App Catalog - ack-arms-prometheus page, select the cluster for which you want to enable Prometheus monitoring in the Deploy section, and click **Create**.

2.  Install the component for container monitoring, ack-arms-cmonitor.

    1.  On the App Catalog page, find and click **ack-arms-cmonitor**.

    2.  On the App Catalog - ack-arms-cmonitor page, select the cluster for which you want to enable container monitoring in the Deploy section, and click **Create**.

        **Note:** The default namespace is arms-prom.


## Enable container monitoring in the ARMS console

1.  Install the component for Prometheus monitoring, ack-arms-prometheus.

    1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

    2.  In the left-side navigation pane, click **Container Monitoring**.

    3.  In the top navigation bar, select the region where your cluster is deployed.

    4.  On the **Container Monitoring** page, click **Mounting** in the **Operation** column of the cluster.

    5.  In the Exporters dialog box, click **Mounting** in the **Operation** column of Prometheus surveillance.

        The App Catalog - ack-arms-prometheus page of the [ACK console](https://cs.console.aliyun.com) appears.

    6.  On the App Catalog - ack-arms-prometheus page, select the cluster for which you want to enable Prometheus monitoring in the Deploy section, and click **Create**.

2.  Install the component for container monitoring, ack-arms-cmonitor.

    1.  On the **Container Monitoring** page, click **Mounting** in the **Operation** column of the cluster.

    2.  In the Exporters dialog box, click **Mounting** in the **Operation** column of Container monitoring.

        The App Catalog - ack-arms-cmonitor page of the [ACK console](https://cs.console.aliyun.com) appears.

    3.  On the App Catalog - ack-arms-cmonitor page, select the cluster for which you want to enable container monitoring in the Deploy section, and click **Create**.

        **Note:** The default namespace is arms-prom.


