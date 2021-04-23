# Create a dashboard for an application monitoring job

Application Real-Time Monitoring Service \(ARMS\) provides the Application Monitoring module to help you troubleshoot issues that occurred within your applications based on the collected monitoring data. To monitor an application in real time, you can create a dashboard for the application monitoring job. The dashboard displays the status of your application in real time.

## Prerequisites

An application monitoring job is created in the ARMS console. For more information, see [Create an application monitoring job](/intl.en-US/Quick Start/Create an application monitoring job.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Dashboards**. On the Dashboards page, choose **Create Dashboard** \> **Custom market** in the upper-right corner.
3.  In the **Create Dashboard** dialog box, enter the dashboard name in the Dashboard Name field and click **OK**. For example, enter App Dashboard. The system creates a blank tab for this dashboard.
4.  Click the pencil icon in the upper part of the tab. In the Tab dialog box, enter the application name in the Tab Name field and click **Save**. For example, enter Tomcat-Demo.

    ![Dashboard Tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4288158061/p43475.png)

5.  Add an application topology.

    1.  In Edit mode, choose **Interactive Control** \> **APM Monitoring Topology** in the upper-right corner of the page.
    2.  In the APM Topology dialog box, set the parameters as required.

        |Parameter|Description|
        |---------|-----------|
        |Name|The name of the topology.|
        |Dataset|The dataset used by the application monitoring job.|
        |Time Globally Controlled|Specifies whether the topology is subject to the global time range that is specified for the application monitoring job. Valid values:        -   **Allow**: The topology displays the data based on the global time range that is specified for the application monitoring job.

**Note:** In Edit mode, you can specify a global time range in the upper-right corner of the page.

        -   **Forbid**: The topology displays the data based on an separate time range instead of the global time range. If you select Forbid, the following two parameters are available:
            -   **Time Span**: the time range of the data to be displayed. You can customize an separate time range for the topology. In this case, the topology is not subject to the global time range.
            -   **Real-Time Data**: specifies whether the topology updates the data to be displayed in real time. Valid values:
                -   **Enable**: The data to be displayed in the topology is updated in real time based on the separate time range that you specified.
                -   **Close**: The data to be displayed in the topology is fixed to that within the separate time range that you specified. |

    3.  Click **OK**.
    **Note:** In Edit mode, you can drag the lower-right corner of the topology to resize it as needed. You can also drag the topology to change its position on the canvas.

6.  Add an application monitoring chart. In Edit mode, choose **Interactive Control** \> **APM Monitoring Graph** in the upper-right corner of the page. In the **New Interactive Chart** dialog box, set the parameters as required and click **OK**. For example, you can select an application site, select **Invocation\_Statistic** from the **Type** drop-down list, select **All** from the **Dimension** drop-down list, and then select **a.Invocation\_count** from the **Metric** drop-down list.

    ![APM Monitoring Graph ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5288158061/p43478.png)

7.  Repeat the preceding step to add two more application monitoring charts. One is used to calculate the response time and the other is used to calculate the number of errors. In the New Interactive Chart dialog box, select the same application site, type, and dimension as in the preceding step, but separately select **a.Invocation\_RT\_ms** and **a.Invocation\_ErrorCount** from the **Metric** drop-down list for the two charts. The following figure shows the created dashboard.

    ![App Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5288158061/p43479.png)

8.  To create dashboards for more applications, click the add icon \(**+**\) in the upper part of the tab, and follow the preceding steps to add application monitoring charts.
9.  To view a dashboard in full-screen mode, perform the following operations: In Edit mode, click **View Mode** and then **Full-screen** in the upper-right corner of the page. In the Full-screen Settings dialog box, select the dashboard that you want to view in full-screen mode and click **OK**.

    **Note:** To switch to the dark theme, click Edit Mode and choose **Theme** \> **Dark** in the upper-right corner of the page.


## References

-   [Create an application monitoring job](/intl.en-US/Quick Start/Create an application monitoring job.md)
-   [Manually install the ARMS agent for a Java application](/intl.en-US/Application Monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md)
-   [Create a dashboard](/intl.en-US/Dashboard and Alerting/Create a dashboard.md)
-   [Manage a dashboard](/intl.en-US/Dashboard and Alerting/Manage a dashboard.md)

