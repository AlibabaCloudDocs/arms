# Troubleshoot exceptions by using diagnostic reports

It is complex and time-consuming to identify and troubleshoot exceptions. Application Real-Time Monitoring Service \(ARMS\) provides the active diagnostics feature to help you identify exceptions such as long response time based on diagnostic reports.

## Step 1: Install the ARMS agent

After you install the ARMS agent, ARMS can conduct all-around monitoring on your applications. Select one of the following methods to install the ARMS agent:

-   For information about how to install the ARMS agent for a Java application, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md).
-   For information about how to install the ARMS agent for a PHP application, see [Install the ARMS agent for a PHP application](/intl.en-US/Application Monitoring/Quick start/Monitor PHP applications/Install the ARMS agent for a PHP application.md).
-   For information about how to install the ARMS agent for an application in Enterprise Distributed Application Service \(EDAS\), see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Enable ARMS to monitor an EDAS application.md).
-   For information about how to install the ARMS agent for an application in a Container Service for Kubernetes \(ACK\) cluster, see [t152230.md\#](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
-   For information about how to install the ARMS agent for an application in an open source Kubernetes environment, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

## Step 2: View the diagnostic report



The installed ARMS agent collects and shows the metrics of applications such as the total number of requests, average response time, number of errors, number of real-time instances, number of full heap garbage collections \(Full GCs\), number of slow SQL queries, number of exceptions, and number of slow calls within the selected period of time. ARMS allows you to view the diagnostic report of all metrics for troubleshooting. You can also view the diagnostic report of a single metric on the Application Overview page.

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

    On the Applications page, if an application has an exception, the **Status** column of the application is displayed in red.

3.  On the Applications page, move the pointer over the row of the application. The **An exception is detected. Click to view details** message appears. Click the red dot to load the diagnostic report. After the diagnostic report is loaded, move the pointer over the red dot and click **Diagnostic Report** to go to the Diagnostic Report page.

    ![Health status of the application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6116268061/p48937.png)

    You can also click the name of the application on the Applications page to go to the Application Overview page. Move the pointer over the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon on the right of **Application Health Overview**. If the **An exception is detected. Click to view details** message appears, click the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon to load the diagnostic report. After the diagnostic report is loaded, click the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon again to go to the Diagnostic Report page.

    ![App health overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8654068061/p180538.png)

4.  On the Diagnostic Report page, view the application name, time range for the diagnostics, symptom, error demarcation, root cause analysis, and detection results of metrics.

    ![Key application events](../images/p48939.png "Diagnostic report")


1.  On the Applications page, click the name of the application to go to the Application Overview page.
2.  On the Application Overview page, drag the pointer over the curve of a metric and select a time period. Click **View report selected time** to go to the Details page.

    ![Diagnostic report for selected time period](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8654068061/p180540.png)

3.  On the Details page, view the detection results of this metric within the selected time range.

    ![Test results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8518168061/p180542.png)


## What to do next

To prevent passive diagnostics after an exception occurs, you can use the alerting feature of ARMS to create an alert for a specific API or all APIs. This ensures that the O&M team receives a notification immediately after an exception occurs.

For more information about how to create an alert, see [Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md).

## References

-   [Create an application monitoring job](/intl.en-US/Quick Start/Create an application monitoring job.md)
-   [t152244.md\#](/intl.en-US/Application Monitoring/Console functions/API monitoring.md)
-   [Trace query](/intl.en-US/Application Monitoring/Console functions/Trace query.md)
-   [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application Monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)
-   [Create ARMS alerts](/intl.en-US/Quick Start/Create ARMS alerts.md)

