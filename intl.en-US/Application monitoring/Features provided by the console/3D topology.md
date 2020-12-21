# 3D topology

3D topology of Application Real-Time Monitoring Service \(ARMS\) can show the health condition of applications, services, and hosts, in addition to the upstream and downstream dependencies of the applications. 3D topology helps you identify the services that caused failures, applications affected by the failures, and associated hosts. This way, you can thoroughly diagnose the root cause of failures and troubleshoot these failures.

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the upper part of the Applications page, select the required region.
3.  On the Applications page, click **3D Topology** of the required application in the **Actions** column.

## Overview

On the Overview page that is displayed by default, you can view all content of the service layer, application layer, and host layer. In the upper-right corner of the page, you can find the number of hosts, applications, and services.

![Overview page of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43101.png)

On the overview layer, you can perform the following operations:

-   In the upper-left corner, click the time range section, and select specific start and end time in the pop-up time picker.
-   In the timeline on the top of the page, drag the slider to change the time range of the current view.
-   In the search box in the upper-right corner of the page, enter your keywords and press the Enter key to search.
-   Drag with your pointer to view the data on all three layers from different angles.
-   Click any object in the view to check metrics related to that object on the right-side panel.

## Service

The service layer shows the services that your applications depend on.

![Service layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43102.png)

Services under each application are grouped into a block. The more the services are called, the bigger their block is. Different statuses of the services are displayed in different colors.

-   : Service calls are normal.
-   : The error rate of the service is relatively high.
-   : No data is returned from the service.

**Note:** The response time threshold of the service is configurable. In the left-side navigation pane, click the triangle icon next to Service to open the threshold setting box. Drag the slider in the setting box to set the threshold.

After you click a service, the right-side panel shows the following information:

-   The name of the service
-   QPS: the queries per second
-   RT\(ms\): the response time in milliseconds
-   ErrQps: the error queries per second

**Note:** In the QPS, RT\(ms\), and Error sections, the left-side numbers are the average value within the selected time range, and the corresponding line chart is on the right side.

## Application

The application layer shows the applications and their upstream and downstream dependencies, including the middleware that the applications and their upstream and downstream depend on. Follow the direction of the connecting lines. You can view the direction in which a call is made.

![Application layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43104.png)

After you click an application, the right-side panel shows the following information of the application:

-   Application name
-   QPS: the queries per second
-   RT\(ms\): the response time in milliseconds
-   ErrQps: the error queries per second

**Note:** In the QPS, RT\(ms\), and Error sections, the left-side numbers are the average value within the selected time range, and the corresponding line chart is on the right side.

## Docker/ECS

The Docker/ECS layer shows the hosts of your applications.

![Host layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43105.png)

Each cube indicates a host. All hosts are grouped by application. Different statuses of the hosts are displayed in different colors.

-   : Normal
-   : Slow
-   : Alerting
-   : Abnormal
-   : Offline

After you click a host, the right-side panel shows the following information of the host:

-   IP address and basic information of the host:
    -   Response time
    -   Number of requests
    -   Number of errors
-   CPU: CPU utilization
-   MEM: memory usage
-   DISK: disk usage
-   GC TIME: the total GC time
-   GC COUNT: the count of GC

**Note:** In the CPU, MEM, and Disk sections, the left-side numbers are the average value within selected time range, while the corresponding line chart is on the right side.

