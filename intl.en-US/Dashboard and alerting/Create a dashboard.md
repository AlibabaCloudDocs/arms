# Create a dashboard

This topic describes how to create a dashboard and configure data for it.

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Dashboards**. On the Dashboards page, choose **Create Dashboard** \> **Custom Dashboard**.
3.  In the **Create Dashboard** dialog box, enter the dashboard name and click **OK**. The new dashboard is displayed in the dashboard list but it does not contain any data. You must configure data for the dashboard.
4.  Add a dataset.

    1.  On the Dashboards page, click **Edit** in the **Actions** column corresponding to the dashboard that you created.
    2.  In the upper-right corner of the page, click **Interactive Control** and select a graph that you want to add.
    3.  In the New Interactive Chart dialog box, enter the chart name, select a **Dataset**, select the chart type, and specify other parameters as needed. Then, click **OK**. For example, if you set Chart Type to Line, the dataset is displayed in line chart.

        ![Composite indicator](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2096143851/p43285.png)

5.  Add a navigation tree.

    1.  On the edit page of the dashboard, choose **Interactive Control** \> **Navigation Tree Components** in the upper-right corner of the page.
    2.  In the Navigation Tree dialog box, enter the **Name** and select the **Dataset Type** and **Dataset**. ARMS automatically imports the multi-dimensional traversal values of this dataset into the **Data** field.
    3.  In the Navigation Tree dialog box, click **OK**. The navigation tree is displayed on the left side of the page.
6.  Associate the dataset with the navigation tree.
    1.  In the data display section, find the chart that you want to manage and click the gear icon in the upper-right corner of the chart.
    2.  In the **Dataset** section of the dialog box, select **Navigation Tree** from the **Dimension** drop-down list, and click **OK**. The dataset is associated with the navigation tree.
7.  View the displayed dataset.

    You can select different dimensions in the navigation tree to view the data of the dataset.

8.  In the time module, select **Today**, **This Week**, or **This Month** to view data within the specified time period. You can also specify the start time and end time.

9.  After the dashboard is configured, click **Save** in the upper-right corner to save the configuration. ARMS automatically saves the configuration every 10 seconds to avoid losing data being edited.

    **Note:**

    -   ARMS automatically saves the configuration every 10 seconds to avoid losing data being edited.
    -   The size and position of the chart in the dashboard can be adjusted.
    -   Adjust the size of a chart

        In edit mode, drag the handle in the lower-right corner of a chart to adjust the size.

    -   Change the position of a chart

        In edit mode, drag a chart to change its position. After you have moved it to the desired position, release the pointer.


