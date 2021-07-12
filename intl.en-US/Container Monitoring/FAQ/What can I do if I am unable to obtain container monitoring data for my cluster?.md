---
keyword: [missing data, container monitoring, enable container monitoring for a cluster]
---

# What can I do if I am unable to obtain container monitoring data for my cluster?

If you cannot obtain the performance data of resources such as Services and Deployments after you install the component for container monitoring on your cluster, container monitoring may fail to be enabled for the cluster. You can troubleshoot this issue based on the procedure provided in this topic.

## Step 1: Check whether the component for container monitoring is installed

1.  Log on to the [Container Service for Kubernetes \(ACK\) console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, click the name of the cluster that you want to manage.

4.  In the left-side navigation pane, choose **Workloads** \> **Jobs**.

5.  On the Jobs page, set the Namespace parameter to kube-system. Then, check whether the cmonitor-post-installer job exists on the Jobs page.

    -   If the cmonitor-post-installer job does not exist, the component for container monitoring is installed on the cluster.
    -   If the cmonitor-post-installer job exists, click the job name and then the Logs tab to view the job logs.
        -   If the job logs contain the error code shown in the following figure, you need to manually attach the two policies that grant full permissions on Application Real-Time Monitoring Service \(ARMS\) and Tracing Analysis to the RAM role of worker nodes in the cluster.

            ![Log of a failure to install the component for container monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9157565261/p286632.png)

        -   If the job logs contain other error codes, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.

## Step 2: Check the status of the agent for container monitoring

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, click the name of the cluster that you want to manage.

4.  In the left-side navigation pane, choose **Workloads** \> **DaemonSets**.

5.  On the DaemonSets page, set the Namespace parameter to arms-prom. Then, check whether the cmonitor-agent DaemonSet exists on the DaemonSets page.

    -   If the cmonitor-agent DaemonSet exists and all the pods involved are ready, the agent for container monitoring is installed on the cluster.

        ![Status of the agent for container monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9157565261/p286796.png)

    -   If the cmonitor-agent DaemonSet does not exist or not all the pods involved are ready, the agent for container monitoring fails to be installed. In this case, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.
6.  Click cmonitor-agent and then the Events tab.

    If an event exists indicating that the readiness probe fails to be installed, container monitoring does not support the kernel version of the host. For more information about the supported kernel versions, see [Environment requirements and limits]().

    ![Exception of the readiness probe](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9157565261/p286842.png)

7.  Click the Logs tab.

    View the pod logs.

    -   If a pod works as expected, logs that contain the version number are continuously generated and no errors are reported.

        ![Logs of a normal pod](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9157565261/p286833.png)

    -   If the following logs are generated, an error occurs within Prometheus Operator. In this case, perform the following steps to restart Prometheus Operator.

        ![Logs of a pod with errors](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6679606261/p287070.png)

        1.  In the left-side navigation pane, choose **Workloads** \> **Pods**.
        2.  On the Pods page, set the Namespace parameter to arms-prom. Then, click **Delete** in the Actions column of the arms-prometheus-\*\*\*\* pod.

            After the pod is deleted, Prometheus Operator is automatically restarted.

    -   If the pod logs contain other error messages, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.

## Step 3: Check the status of Prometheus Operator

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, click the name of the cluster that you want to manage.

4.  In the left-side navigation pane of the details page, choose **Workloads** \> **Deployments**.

5.  On the Deployments page, set the Namespace parameter to arms-prom. Then, check whether the arms-prom-ack-arms-prometheus Deployment exists on the Deployments page.

    -   If the Deployment exists and all the pods involved are ready, Prometheus Operator works as expected.

        ![Container monitoring - Deployments - Status of Prometheus Operator](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9157565261/p286835.png)

    -   If the Deployment does not exist or not all the pods involved are ready, the agent for container monitoring fails to be installed. In this case, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.
6.  Click arms-prom-ack-arms-prometheus and then the Logs tab.

    View the pod logs. If the pod logs contain error messages, you can join the official DingTalk group for container monitoring \(group ID: `31588365`\) to seek help.




