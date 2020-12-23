# Create a dashboard for an application monitoring job

Application Real-Time Monitoring Service \(ARMS\) provides the Application Monitoring module to help you troubleshoot your applications based on the collected monitoring data. To monitor an application in real time, you can create a dashboard for the application monitoring job. The dashboard displays the status of your application in real time.

## Prerequisites

An application monitoring job is created in the ARMS console. For more information, see [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Dashboards**. On the Dashboards page, choose **Create Dashboard** \> **Custom Dashboard** in the upper-right corner.
3.  In the **Create Dashboard** dialog box, enter the dashboard name and click **OK**. For example, enter App Dashboard. The system creates a blank tab for this dashboard.
4.  Click the pencil icon on the top of the tab. In the Tab dialog box, enter the application name in the Tab Name field and click **Save**. For example, enter Tomcat-Demo.

    ![Dashboard Tab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4288158061/p43475.png)

5.  Add an application topology. In Edit mode, choose **Interactive Control** \> **APM Monitoring Topology** in the upper-right corner of the page. In the APM Topology dialog box, enter the topology name, select a dataset of the application monitoring job, and then click **OK**.

    ![APM Monitoring Topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4288158061/p43476.png)

    **Note:** Drag the lower-right corner of a chart to resize it as needed. Drag the chart to change its position.

    ![APM Monitoring Topology](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5288158061/p43477.png)

6.  Add an application monitoring chart. In Edit mode, choose **Interactive Control** \> **APM Monitoring Graph** in the upper-right corner of the page. In the **New Interactive Chart** dialog box, set all the required parameters and click **OK**. For example, after you select an application site, select **Invocation\_Statistic** from the **Type** drop-down list, select **All** from the **Dimension** drop-down list, and select **a.Invocation\_count** from the **Metric** drop-down list.

    ![APM Monitoring Graph ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5288158061/p43478.png)

7.  Repeat the preceding step to add two more application monitoring charts. One is used to calculate the response time and the other is used to calculate errors. In the New Interactive Chart dialog box, select the same application site, type, and dimension as in the preceding step, but select **a.Invocation\_RT\_ms** and **a.Invocation\_ErrorCount** from the **Metric** drop-down list. The following figure shows the created dashboard.

    ![App Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5288158061/p43479.png)

8.  To create dashboards for more applications, click the add icon \(**+**\) on the top of the tab, and follow the preceding steps to add more application monitoring charts.
9.  In Edit mode, click **View Mode** in the upper-right corner and click **Full-screen**. The dashboard appears in full-screen mode.

    **Note:** To switch to the dark theme, click Edit Mode and choose **Theme** \> **Dark** in the upper-right corner of the page.


## References

-   [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)
-   [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md)
-   [Create a dashboard](/intl.en-US/Dashboard and alerting/Create a dashboard.md)
-   [Manage a dashboard](/intl.en-US/Dashboard and alerting/Manage a dashboard.md)

