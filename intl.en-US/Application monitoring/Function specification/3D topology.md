# 3D topology

The application monitoring function of Application Real-Time Monitoring Service provides the 3D topology, which shows the health condition of applications, services, and hosts, in addition to the upstream and downstream dependencies of the applications. With the 3D topology, you can quickly identify the services that caused failures, applications influenced by the failures, and associated hosts. This enables you to thoroughly investigate the root cause of the failures, and then fix the issues quickly.

## Portal

Follow these steps to access the 3D topology function in ARMS application monitoring.

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, take the following actions as needed.

    -   To view the 3D topology of all applications, click **View 3D Topology of All Applications \(Beta\)** at the top.

    -   To view the 3D topology of a specific application, find the application and click **3D Topology** in the **Actions** column.


## Overview

On the Overview page that appears by default, you can see all the content of the service layer, application layer, and host layer. In the upper-right corner of the page, you can find the number of hosts, applications, and services.

![ARMS 3D拓扑图Overview页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43101.png)

On the overview layer, you can perform the following operations:

-   In the upper-left corner, click the time range section, and select the specific start time and end time in the time picker that appears.
-   In the timeline at the top of the page, drag the slider to change the time range of the current view.
-   In the search box in the upper-right corner of the page, enter your keywords and press Enter to search.
-   Drag with your mouse to view the data on all three layers from different dimensions.
-   Click any object in the view to check metrics related to that object on the right-side panel.

## Service

The service layer shows the services that your applications depend on.

![ARMS 3D拓扑图服务层](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43102.png)

Services under each application are grouped into a block. The more the services are called, the bigger their block is. Different states of the services are indicated in different colors.

-   : Service calls are normal.
-   : The error rate of the service is relatively high.
-   : No data is returned from the service.

**Note:** The response time threshold of services is configurable. In the left-side navigation pane, click the triangle icon next to Service to open the Threshold Settings box. Drag the slider in the Threshold Settings box to set the threshold.

After you click a service, the right-side panel shows the following information:

-   The name of the service
-   QPS: the queries per second
-   RT\(ms\): the response time in milliseconds
-   ErrQps: the error queries per second

**Note:** In the QPS, RT, and ErrQps sections, the left-side numbers are the average value within the selected time range, and the corresponding line chart is on the right side.

## Application

The application layer shows the applications and their upstream and downstream dependencies, including the middleware they depend on. By checking the direction of the connecting lines, you can determine the calling and called objects.

![ARMS 3D拓扑图应用层](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6952628061/p43104.png)

After you click an application, the right-side panel shows the following information of that application:

-   Application Name
-   QPS: the queries per second
-   RT\(ms\): the response time in milliseconds
-   ErrQps: the error queries per second

**Note:** In the QPS, RT, and ErrQps sections, the left-side numbers are the average value within the selected time range, and the corresponding line chart is on the right side.

## Docker/ECS

The Docker/ECS layer shows the host information of your applications.

![ARMS 3D拓扑图主机层](../images/p43105.png "Host layer of ARMS 3D Topology")

Each cube is a host. All hosts are grouped by applications. Different states of the hosts are indicated in different colors.

-   : Normal
-   : Slow
-   : Alerting
-   : Abnormal
-   : Offline

After you click a host, the right-side panel shows the following information of that host:

-   IP address and basic information of the host:
    -   IDC
    -   Unit
    -   Host
    -   CPU: Number of CPU cores
    -   JVM: JVM version
    -   Tomcat: Tomcat version
-   CPU: CPU usage
-   MEM: Memory usage
-   LOAD: Load

**Note:** In the CPU, MEM, and LOAD sections, the left-side numbers are the average value within the selected time range, and the corresponding line chart is on the right side.

