# Application overview

On the Application Overview page, you can view the health metrics of an application.You can view the upstream and downstream dependent components of an application in an application topology graph. You can also view the health status of the application, services, and hosts in a 3D topology.The health metrics of an application include general metrics such as Total Requests and Average Response Time, metrics related to the application services and dependent services, and system information such as the CPU utilization and memory usage.

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Application**, and select a region in the top navigation bar.
3.  On the Applications page, click the application that you want to view to go to the Application Overview page.

    On the Application Overview page, view information on the **Overview**, **Topology**, and **3D Topology \(Beta\)** tabs.


## Overview

The following key metrics are displayed on the Overview tab:

-   Total Requests, Average Response Time, Errors,Real Time Instance Count, Full GC, Slow SQL, Exceptions, Thread Profiling. You can also check how the values of these metrics have changed since the last week or last day on this tab.
-   Application Events: application events, such as 0-1 alerts, application monitoring alerts, and Kubernetes cluster events.
-   Application Support Services: time sequence curves for Application Service Request and Application Service Average Response Time.
-   Application Dependent Services: time sequence curves for Application Dependent Service Request, Application Dependent Service Average Response Time, App Instance Count, and HTTP - Status Code.
-   System Info: time sequence curves for CPU, MEM, and Load.
-   Thread Profiling: time sequence curves and details about Slow Calls.
-   Statistical Analysis: analysis on Interface with Slow Calls and Exception.

![Application Monitoring > Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2017358061/p43127.png)

## Application topology

On the Topology tab, you can obtain a better view of the upstream and downstream components of your application and the call relationship between the components and the application. Then, you can identify the bottlenecks of your application.

![Application Monitoring > Topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2017358061/p43129.png)

## 3D Topology

On the 3D Topology \(Beta\) tab, the health status of an application, services, and hosts, and the upstream and downstream dependencies of the application are displayed. You can use the 3D topology to identify the services that caused failures, applications affected by the failures, and associated hosts. The 3D topology helps you diagnose the root causes of failures and troubleshoot these failures. For more information about 3D topology, see [3D topology](/intl.en-US/Application monitoring/Features provided by the console/3D topology.md).

![Application Monitoring > 3D Topology (Beta)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6920658061/p46742.png)

