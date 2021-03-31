# Monitor applications deployed on Container Service for Kubernetes

The business transaction feature provided by Application Real-Time Monitoring Service \(ARMS\) allows you to define business requests in a visualized manner by using non-intrusive methods and provides abundant business-specific performance metrics and diagnostic capabilities. Before you use the business transaction feature, you must install or upgrade the ARMS agent for Java applications.

## Limits

-   The business transaction feature can only monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Procedure

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8684574161/p103004.png)

**Note:** Scan the following QR code to join the DingTalk group.

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5000817161/p92785.png)

## Install the ARMS agent for Java applications in Container Service for Kubernetes

If you are using the business transaction feature for the first time and have not used the application monitoring feature, you must install the latest version of the ARMS agent. For more information, see [Install the ARMS agent for a Java application deployed in Container Service for Kubernetes](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).

## Upgrade the ARMS agent for Java applications in Container Service for Kubernetes

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later.

1.  Log on to the [Container Service for Kubernetes console](https://partners-intl.console.aliyun.com/#/cs).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the **Clusters** page, click the ID of the cluster where your application is deployed.

4.  In the left-side navigation pane, choose **Applications** \> **Helm**.

    ![tab_business_helm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8780240161/p93070.png)

    -   If the arms-pilot component was updated earlier than December 1, 2019, you must upgrade the arms-pilot component before you can upgrade the ARMS agent. Go to [Step 5](#step_zth_q9r_1kt).
    -   If the arms-pilot component was updated later than December 1, 2019 \(inclusive\), go to [Step 7](#step_ud6_l2w_izu).
5.  In the left-side navigation pane, choose **Workloads** \> **Pods**.

6.  On the **Pods** page, select **arms-pilot** from the **Namespace** drop-down list. Find the pod corresponding to the arms-pilot component and click **Delete** in the Actions column.

    After the pod is deleted, a new pod is automatically created.

7.  Restart your business pod.

    The ARMS agent is automatically updated.

8.  Run the `cat /home/admin/.opt/ArmsAgent/version` command in the container to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


**Related topics**  


[Preparations](/intl.en-US/Business Monitoring/Monitor Java applications/Preparations.md)

