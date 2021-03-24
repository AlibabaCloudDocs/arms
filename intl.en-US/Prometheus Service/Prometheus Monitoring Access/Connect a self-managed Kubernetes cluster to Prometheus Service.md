# Connect a self-managed Kubernetes cluster to Prometheus Service

This topic describes how to connect a self-managed or third-party Kubernetes cluster to Prometheus Service. Then, you can use predefined dashboards to monitor multiple performance metrics of servers and the Kubernetes cluster.

-   A Kubernetes cluster is created. For more information, see [Create a Cluster](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/).
-   Application Real-Time Monitoring Service \(ARMS\) is activated. For more information, see [Activate and upgrade ARMS](/intl.en-US/Quick Start/Activate and upgrade ARMS.md).

## Enable Prometheus Service

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select a region. Then, click **Access prometheus monitoring** in the upper-right corner.

4.  On the **Access Prometheus monitoring** page, click **Self-built Kubernetes cluster**.

5.  In the **Access a self-built Kubernetes cluster** dialog box, perform the following steps:

    1.  In Step 1, enter the name of the self-managed Kubernetes cluster that you want to connect to Prometheus Service and click **Next**.

        ![custom-test-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2031556161/p253266.png)

    2.  Log on to the Kubernetes cluster and run the command that is shown in Step 2. Then, click **Next**.

        ![custom-test-2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2031556161/p253268.png)

    3.  Run the command that is shown in Step 3.

        ![custom-3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2031556161/p253271.png)

    Then, the **Prometheus Monitoring** page displays the Kubernetes cluster that is connected to Prometheus Service.


## Go to a Grafana dashboard

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select a region. Then, click the dashboard that you want to view in the **Installed Dashboards** column.


## Uninstall the Prometheus agent

To disable Prometheus Service for a self-managed Kubernetes cluster, perform the following steps to uninstall the Prometheus agent:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select a region. Then, find the Kubernetes cluster for which you want to uninstall the Prometheus agent and click **Uninstall** in the **Actions** column.

4.  In the **Confirmation** message, click **OK**.

    After you uninstall the Prometheus agent, the dashboards of the Kubernetes cluster disappear from the **Installed Dashboards** column.


