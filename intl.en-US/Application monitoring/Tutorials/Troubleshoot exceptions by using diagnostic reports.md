# Troubleshoot exceptions by using diagnostic reports

It is a complex and time-consuming task to identify and troubleshoot exceptions. Application Real-Time Monitoring Service \(ARMS\) provides the active diagnostics feature to help you identify exceptions such as long response time.

## Step 1: Install an ARMS agent

After you install an ARMS agent, ARMS can conduct all-around monitoring of your applications. Select one of the following methods to install an ARMS agent.

-   To install an ARMS agent for Java applications, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md).
-   To install an ARMS agent for PHP applications, see [Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md).
-   To install an ARMS agent for applications in EDAS, see [Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Start monitoring Java applications/Enable ARMS to monitor an EDAS application.md).
-   To install an ARMS agent for applications in Container Service for Kubernetes, see [t152230.md\#](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
-   To install an ARMS agent for applications in open source Kubernetes environments, see [Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for an application deployed in an open source Kubernetes environment.md).

## Step 2: View the diagnostic report



The installed ARMS agent collects and shows the metrics of applications such as Total Requests, Average Response Time, Errors, Real Time Instance Count, Full GC, Slow SQL, Exceptions, and Thread Profiling within the selected period of time. ARMS allows you to view the diagnostic report of troubleshooting metrics. You can also view the diagnostic report of a single metric on the Application Overview page.

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

    On the Applications page, if the application has an exception, the **Status** column is displayed in red.

2.  On the Applications page, move the pointer over the row of the application. The **An exception is detected. Click to view details** message appears. Click the red dot to load the diagnostic report. After the diagnostic report is loaded, move the pointer over the red dot and click **Diagnostic Report** to go to the Diagnostic Report page.

    ![Health status of the application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8654068061/p48937.png)

    You can also click the name of the application on the Applications page to go to the Application Overview page. Move the pointer over the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon on the right of **Application Health Overview**. If the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png)**An exception is detected. Click to view details** message appears, click the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon to load the diagnostic report. After the diagnostic report is loaded, click the ![health](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7518168061/p180537.png) icon again to go to the Diagnostic Report page.

    ![App health overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8654068061/p180538.png)

3.  On the Diagnostic Report page, view the application name, diagnostic time, symptom, error demarcation, root cause analysis, and detection results of metrics.

    ![Key application events](../images/p48939.png "Diagnostic report")


1.  On the Applications page, click the name of the application to go to the Application Overview page.
2.  On the Application Overview page, drag the pointer over the curve of a metric and select a time period. Click **View report of selected time** to go to the Details page.

    ![Diagnostic report for selected time period](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8654068061/p180540.png)

3.  On the Details page, view the detection results of this metric for the selected time range.

    ![Test results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8518168061/p180542.png)


## What to do next

To avoid passive diagnostics after an exception occurs, you can also use the alert feature of ARMS to create an alert for API operations. This ensures that the O&M team receives a notification in real time after an exception occurs.

To create an alert, see [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md).

## References

-   [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)
-   [t152244.md\#](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md)
-   [Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md)
-   [Analyze errors in code by using ARMS thread profiling](/intl.en-US/Application monitoring/Tutorials/Analyze errors in code by using ARMS thread profiling.md)
-   [Create ARMS alerts](/intl.en-US/Quick start/Create ARMS alerts.md)

