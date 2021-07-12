---
keyword: [container monitoring, Kubernetes, ACK]
---

# Disable container monitoring

If you no longer need to use container monitoring, you can uninstall the component for container monitoring from your Kubernetes cluster. This topic shows you how to uninstall the component for container monitoring from a Kubernetes cluster to disable container monitoring.

## Procedure

1.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

2.  On the Clusters page, click the name of the Kubernetes cluster for which you want to disable container monitoring.

3.  In the left-side navigation pane, choose **Applications** \> **Helm**.

4.  On the Helm page, find arms-cmonitor and click **Delete** in the Actions column.

5.  In the Delete dialog box, click **OK**.

    After you uninstall the component, the cluster name is dimmed on the Container Monitoring page in the Application Real-Time Monitoring Service \(ARMS\) console. You cannot click the cluster name to view the monitoring data.


## Verify the result

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Container Monitoring**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  On the **Container Monitoring** page, check the status of the cluster.

    If the cluster name is dimmed on this page, the component for container monitoring is uninstalled from the cluster. You cannot click the cluster name to view the monitoring data.


## Contact us

If you have questions when you use container monitoring, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.

