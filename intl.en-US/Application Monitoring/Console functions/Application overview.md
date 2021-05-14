# Application overview

On the Application Overview page, you can view the key metrics, upstream and downstream dependent components, and 3D topology of the selected application. This page shows the overall health status of your application.

## Go to the Application Overview page

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.
3.  On the Applications page, click the name of the application that you want to view to go to the Application Overview page.

    On the Application Overview page, view information on the **Overview**, **Topology**, and **3D Topology \(Beta\)** tabs.


## Overall tab

The Overall tab displays the following key metrics:

-   Total Requests, Average Response Time, Errors,Instance Count, Full GC, Exceptions, Thread Profiling, and Slow SQL. You can also check how the values of these metrics have changed since the last week or last day on this tab.
-   Application Events: application events, such as 0-1 alerts, application monitoring alerts, and Kubernetes cluster events.
-   Application Support Services: time series curves for the number of requests to the services provided by the application and average response time.
-   Application Dependent Services: time series curves for the number of requests to the dependent services, average response time, number of instances within the application, and HTTP status codes.
-   System Info: time series curves for CPU utilization, memory usage, and load.
-   Thread Profiling: time series curves and details of slow calls.
-   Statistical Analysis: analysis on slow API calls and exception types.

![Application Monitoring > Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2017358061/p43127.png)

## Topology tab

On the Topology tab, you can view the upstream and downstream components of your application and the call relationship between the components and the application in the topology. The topology helps you identify the bottlenecks of your application.

![Application Monitoring > Topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2017358061/p43129.png)

## 3D Topology \(Beta\) tab

On the 3D Topology \(Beta\) tab, you can view the health status of your application, services, and hosts, and the upstream and downstream dependencies of the application. You can use the 3D topology to identify the services that caused failures, applications affected by the failures, and associated hosts. This way, you can thoroughly diagnose the root cause of failures and troubleshoot these failures. For more information about the 3D topology, see [3D topology](/intl.en-US/Application Monitoring/Console functions/3D topology.md).

![Application Monitoring > 3D Topology (Beta)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6920658061/p46742.png)

