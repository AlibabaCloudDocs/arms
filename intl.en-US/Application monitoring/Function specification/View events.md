# View events

EDAS allows you to view event information, alert information, diagnosis reports, and microservice governance information of Kubernetes-native applications, which helps you understand the application running status and quickly focus on problems.

## Portal of Event Center

1.  Log on to the [EDAS console](https://edas-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Resources** \> **Clusters**. On the Cluster Details page, click the application name in **Applications**.

    You can also choose **Application Management** \> **Applications** from the left-side navigation pane, and then click the name of the Container Service Kubernetes application on the **Applications** page.

3.  In the left-side navigation pane of the Application Overview page, click **Event Center**.


## View Kubernetes events

1.  On the **Event Center** page, click the **K8s Events** tab.

2.  On the **K8s Events** tab page, set the event search conditions, and then click Refresh button.

    Current search conditions are as follows:

    -   **Kind**: includes **Application Instance \(Pod\)**, **SLB \(Service\)**, **Application \(Deployment\)**, and **Auto Scaling \(HorizontalPodAutoscaler\)**.
    -   **Cause**: allows you to select the cause for an event, such as FailedScheduling.
    -   **Pod**: allows you to select the target pod.
    -   **Level**: includes Warning and Normal.
    **Note:** If a **Warning** event exists, pay special attention to the event and check your application.


## View application alerts

The **Application Alerts** tab displays information such as the alert ID, alert name, alert event, and alert content.

## View application diagnosis

On the **Diagnosis Reports** tab, you can filter diagnosis reports by **Report Type**. You can also click ![Diagnosis report icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1755166951/p72385.png) in the upper part of the **Application Overview** page.

## View microservice governance details

The **Microservice Governance** tab displays all microservice governance details of the application, such as the governance time, governance type, and governance object.

