# Monitor applications deployed on Alibaba Cloud Container Service for Kubernetes

The business transaction feature provided by ARMS allows you to define business requests in a visualized manner by using non-intrusive methods and provides abundant business-specific performance metrics and diagnostic capabilities. Before you use the business transaction feature, you must install or upgrade the ARMS agent for Java applications.

## Limits

-   The business transaction feature only can monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Install the ARMS agent for Java applications in Alibaba Cloud Container Service for Kubernetes

If you are using the business transaction feature for the first time and have not used the application monitoring feature, you must install the latest version of the ARMS agent. For more information, see [Install the ARMS agent for a Java application deployed in Container Service for Kubernetes](/intl.en-US/Application monitoring/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).

## Upgrade the ARMS agent for Java applications in Alibaba Cloud Container Service for Kubernetes

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later.

1.  Log on to the [Container Service for Kubernetes console](https://partners-intl.console.aliyun.com/#/cs). In the left-side navigation bar, choose **Applications** \> **Releases**. Click the Helm tab to view the update time of the ack-arms-pilot component.

    ![tab_business_helm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3583758061/p93070.png)

    -   If the update time is earlier than December 2019, you must upgrade the ack-arms-pilot components before you can upgrade the ARMS agent. Perform [Step 32](#step_zth_q9r_1kt).
    -   If the update time is later than December, 2019 \(inclusive\), perform [Step 44](#step_ud6_l2w_izu) directly.
2.  In the left-side navigation pane, choose **Clusters** \> **Clusters**. On the Clusters page, find the cluster, and click **Dashboard** in the **Actions** column.

    ![pg_business_ack_cluster_list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3827258061/p91060.png)

3.  In the left-side navigation pane, click **Namespaces**. Select **arms-pilot** or **arms-pilot-system** from the list. In the **Pod** section of the Overview page, choose the icon \> **Delete** to delete the pod of the arms-pilot component.

    ![sc_business_delete_pods](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4827258061/p91078.png)

    After the pod is deleted, a new pod is automatically created.

4.  Restart your business pod.

    The ARMS agent is automatically updated.

5.  Run the `cat /home/admin/.opt/ArmsAgent/version` command in the container to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


