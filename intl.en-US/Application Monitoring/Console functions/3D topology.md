# 3D topology

The 3D topology of Application Real-Time Monitoring Service \(ARMS\) can show the health status of applications, services, and hosts, in addition to the upstream and downstream dependencies of the applications. You can use the 3D topology to identify the services that caused failures, applications affected by the failures, and associated hosts. This way, you can thoroughly diagnose the root cause of failures and troubleshoot these failures.

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. On the Applications page, select a region in the top navigation bar.
3.  On the Applications page, click **3D Topology** in the **Actions** column of the required application.

## Overview

On the Overview page that is displayed by default, you can view all content of the service layer, application layer, and host layer. In the upper-right corner of the page, you can view the numbers of hosts, applications, and services.

![Overview page of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43101.png)

On the Overview page, you can perform the following operations:

-   In the upper-left corner, click the time range section, and select specific start and end time in the pop-up time picker.
-   In the timeline in the upper part of the page, drag the slider to change the time range of the current topology.
-   In the search box in the upper-right corner of the page, enter a keyword and press the Enter key to search for applications.
-   Drag the topology with your pointer to view the data on all three layers from different angles.
-   Click an object in the topology to check the metrics related to the object in the right-side pane.

## Service layer

The service layer shows the services that your applications depend on.

![Service layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43102.png)

Services under each application are grouped into a block. The more times a service is called, the larger area it occupies in its block. Different statuses of the services are indicated in different colors.

-   : Service calls are normal.
-   : The error rate of the service is relatively high.
-   : No data is returned from the service.

**Note:** You can set the threshold of the service response time by performing the following steps: In the left-side navigation pane, click the triangle icon next to Service to open the threshold setting box. Drag the slider in the setting box to set the threshold.

After you click a service, the right-side pane shows the following information:

-   Service name
-   QPS: the number of queries per second
-   RT\(ms\): the response time in milliseconds
-   Error: the number of failed queries per second

**Note:** In the QPS, RT\(ms\), and Error sections, the left-side numbers are the average values within the selected time range, and the corresponding line charts are on the right side.

## Application layer

The application layer shows the applications and their upstream and downstream dependencies, including the middleware that the applications and their upstream and downstream applications depend on. Follow the direction of the connecting lines. You can view the direction in which a call is made.

![Application layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43104.png)

After you click an application, the right-side pane shows the following information of the application:

-   Application name
-   QPS: the number of queries per second
-   RT\(ms\): the response time in milliseconds
-   Error: the number of failed queries per second

**Note:** In the QPS, RT\(ms\), and Error sections, the left-side numbers are the average values within the selected time range, and the corresponding line charts are on the right side.

## Docker/ECS layer

The Docker/ECS layer is the host layer. It shows the hosts of your applications.

![Host layer of ARMS 3D topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43105.png)

Each cube indicates a host. All hosts are grouped by application. Different statuses of the hosts are displayed in different colors.

-   : Normal
-   : Slow
-   : Alerting
-   : Abnormal
-   : Offline

After you click a host, the right-side pane shows the following information of the host:

-   IP address and basic information of the host:
    -   Response time
    -   Number of requests
    -   Number of errors
-   CPU: CPU utilization
-   MEM: memory usage
-   DISK: disk usage
-   GC TIME: the total time consumed by garbage collections \(GCs\)
-   GC COUNT: the number of GCs

**Note:** In the CPU, MEM, and DISK sections, the left-side numbers are the average values within the selected time range, and the corresponding line charts are on the right side.

