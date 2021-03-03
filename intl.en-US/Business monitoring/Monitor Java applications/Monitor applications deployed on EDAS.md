# Monitor applications deployed on EDAS

The business transaction feature provided by Application Real-Time Monitoring Service \(ARMS\) allows you to define business requests in a visualized manner by using non-intrusive methods and provides abundant business-specific performance metrics and diagnostic capabilities. Before you use the business transaction feature, you must install or upgrade the ARMS agent for Java applications.

## Limits

-   The business transaction feature can only monitor Java applications.
-   Only the ARMS agent V2.6.2 or later supports the business transaction feature.

## Procedure

![dg_business_workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8684574161/p103004.png)

**Note:** Scan the following QR code to join the DingTalk group.

![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7037258061/p92785.png)

## Install the ARMS agent for Java applications deployed on EDAS

If you are using the business transaction feature for the first time and have not used the application monitoring feature, you must install the latest version of the ARMS agent. For more information, see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Enable ARMS to monitor an EDAS application.md).

## Upgrade the ARMS agent for Java applications deployed on ECS clusters in EDAS

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later. To upgrade the ARMS agent for Java applications deployed on ECS clusters in EDAS, perform the following steps:

1.  Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Application Management** \> **Applications**.

3.  In the top navigation bar, select the region where your application is deployed.

4.  On the **Applications** page, click the name of the application for which you want to enable the business transaction feature.

5.  On the page that appears, click **Deploy Application** in the upper-right corner and deploy the application.

    For more information about how to deploy an application, see [t1838948.md\#section\_d2h\_972\_4zb]().

    After the application is deployed, the ARMS agent is automatically upgraded.

6.  Connect to the ECS instance and log on to it. Run the `cat /home/admin/.opt/ArmsAgent/version` command to check the version of the ARMS agent.

    For more information about how to connect to and log on to an ECS instance, see [OverviewGuidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


## Upgrade the ARMS agent for Java applications deployed on Kubernetes clusters in EDAS

If you are using the business transaction feature for the first time and have used the application monitoring feature, you must upgrade the ARMS agent to V2.6.2 or later. When you upgrade the ARMS agent for Java applications deployed on Kubernetes clusters in EDAS, you must take note of the time when Kubernetes clusters were imported to EDAS. The upgrade operations differ for Kubernetes clusters imported to EDAS before and after December 2019.

1.  Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Resource Management** \> **Container Service Kubernetes Clusters**.

3.  In the top navigation bar, select the region where your application is deployed.

4.  On the **Container Service Kubernetes Cluster** page, click the ID of the cluster where your application is deployed.

5.  On the **Cluster Details** page, click **View Details** in the **Cluster Information** section.

    -   If the cluster was created earlier than December 1, 2019, you must upgrade the arms-pilot component before you can upgrade the ARMS agent. Go to [Step 6](#step_b44_68o_1pf).
    -   If the cluster was created later than December 1, 2019 \(inclusive\), go to [Step 10](#step_w77_b7m_zrc).
6.  Log on to the [Container Service for Kubernetes console](https://partners-intl.console.aliyun.com/#/cs).

7.  On the Clusters page, click the name of the cluster where your application is deployed.

8.  In the left-side navigation pane, choose **Workloads** \> **Pods**.

9.  On the **Pods** page, select **arms-pilot** from the **Namespace** drop-down list. Find the pod corresponding to the arms-pilot component and click **Delete** in the Actions column.

    After the pod is deleted, a new pod is automatically created.

10. Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

11. In the left-side navigation pane, choose **Application Management** \> **Applications**.

12. In the top navigation bar, select the region where your application is deployed.

13. On the **Applications** page, click the name of the application for which you want to enable the business transaction feature.

14. On the **Application Overview** page, choose **Deploy** \> **Deploy** in the upper-right corner and deploy the application.

    For more information about how to deploy an application, see [Batch release \(applicable to Kubernetes clusters\)]() or [Canary release \(Kubernetes clusters\)]().

    After the application is deployed, the ARMS agent is automatically upgraded.

15. On the **Application Overview** page, click Running Pods \(Click View\) to the right of **Running Status** in the **Basic Information** section. In the **App Configurations** pane, find the pod and click **Terminal** in the **Actions** column. Run the `cat /home/admin/.opt/ArmsAgent/version` command to check the version of the ARMS agent.

    If the version number starts with 2.6.2, the ARMS agent has been upgraded to V2.6.2 or later. You can create a business transaction task to monitor your applications.


**Related topics**  


[Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Enable ARMS to monitor an EDAS application.md)

