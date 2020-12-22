# Monitor applications deployed on EDAS

The business transaction feature provided by ARMS allows you to define business requests in a visualized manner by using non-intrusive methods and provides abundant business-specific performance metrics and diagnostic capabilities. Before you use the business transaction feature, you must install or upgrade the ARMS agent for Java applications.

## Limits

-   The business transaction feature only can monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Install the ARMS agent for Java applications deployed on EDAS

If you are using the business transaction feature for the first time and have not used the application monitoring feature, you must install the latest version of the ARMS agent. For more information, see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Start monitoring Java applications/Enable ARMS to monitor an EDAS application.md).

## Upgrade the ARMS agent for Java applications deployed on ECS clusters in EDAS

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later. To upgrade the ARMS agent for Java applications deployed on ECS clusters in EDAS, perform the following steps:

1.  Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Application Management** \> **Applications**. Click the application for which you want to enable the business transaction feature of ARMS.

    The Application Details page appears.

3.  In the left-side navigation pane, click **Basic Information**. On the Basic Information page, click **Deploy Application** in the upper-right corner to deploy the application. For more information, see [t1838948.md\#section\_d2h\_972\_4zb]().

    ![tab_business_deployment_detail](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3827258061/p88780.png)

    After the application is deployed, the ARMS agent is automatically updated.

4.  Connect to the ECS instance and log on to it. For more information, see [OverviewGuidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md). Run the `cat /home/admin/.opt/ArmsAgent/version` command to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


## Upgrade the ARMS agent for Java applications deployed on Kubernetes clusters in EDAS

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later. When you upgrade the ARMS agent for Java applications deployed on Kubernetes clusters in EDAS, you must take note of the time when Kubernetes clusters were imported to EDAS. The upgrade operations differ for Kubernetes clusters imported to EDAS before and after December 2019.

1.  Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Resource Management** \> **Container Service Kubernetes Cluster**. On the Container Service Kubernetes Cluster page, find the cluster and view the information in the **Created At** column.

    -   If the cluster was created earlier than December 2019, you must upgrade the ack-arms-pilot components before you can upgrade the ARMS agent. Perform [Step 3](#step_b44_68o_1pf).
    -   If the cluster was created later than December, 2019 \(inclusive\), perform [Step 6](#step_5kr_tre_5pi) directly.
3.  On the Container Service Kubernetes Cluster page, click the cluster ID in the **Cluster ID/Name** column to go to the Cluster Details page. Copy the information of the **csClusterId** field in the **Cluster Information** section.

4.  Log on to the[Container Service for Kubernetes console](https://partners-intl.console.aliyun.com/#/cs). In the left-side navigation pane, choose Clusters. Select **ID** from the **Name** drop-down list in the upper part and paste the information of the **csClusterId** field that you have copied to the next box. After the Kubernetes cluster is automatically searched and displayed on the page. Click **Console** in the **Actions** column.

    ![pg_business_ack_cluster_list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3827258061/p91060.png)

5.  In the left-side navigation pane, click **Namespaces**. Select **arms-pilot** or **arms-pilot-system** from the list. In the **Pod** section of the Overview page, choose the icon \> **Delete** to delete the pod of the arms-pilot component.

    ![sc_business_delete_pods](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4827258061/p91078.png)

    After the pod is deleted, a new pod is automatically created.

6.  Log on to the[EDAS console](https://edas-intl.console.aliyun.com). In the left-side navigation pane, choose **Application Management** \> **Applications**. Click the application for which you want to enable the business transaction feature of ARMS.

7.  On the Application Overview page, click **Deploy Application** or **Deploy Historical Version** in the upper-right corner to deploy the application. For more information, see [Batch release \(applicable to Kubernetes clusters\)]() or [Canary release \(Kubernetes clusters\)]().

    After the application is deployed, the ARMS agent is automatically updated.

8.  In the **Pod Information** section of the Application Overview page, click **Terminal** section and run the `cat /home/admin/.opt/ArmsAgent/version` command to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


**Related topics**  


[Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Start monitoring Java applications/Enable ARMS to monitor an EDAS application.md)

