# Create an interactive dashboard

To create an interactive dashboard, follow these steps: create an interactive dashboard and configure the dashboard data.

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click**Interactive Dashboard**, And then chooseInteractive dashboard managementPage, select**Create an interactive dashboard** \> **Custom dashboard**.
3.  In**Create an interactive dashboard**Dialog box, enter the name of the interactive dashboard and click**OK**. The new interactive dashboard is displayed in the interactive dashboard management page, but there is no data, then you need to configure data for the dashboard.
4.  Add a dataset.

    1.  On the interactive dashboard management page, click the right side of the dashboard name**Operation**Column**Edit**.
    2.  Click**Interaction Control**And select Add Chart type.
    3.  In the create interactive chart dialog box, enter a chart name and select**Dataset**, Select the chart type, enter other optional information as needed, and click**OK**. For example, you can select the line chart type to view the line chart display of the dataset in the data display area.

        ![Composite indicator](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2096143851/p43285.png)

5.  Add a navigation tree.

    1.  On the dashboard editing page, select**Interaction Control** \> **Navigation tree control**.
    2.  In the navigation tree dialog box, enter**Name**And Select**Dataset type**And**Dataset**. ARMS automatically imports the multi-dimensional traversal value of the dataset to**Data**Text box.
    3.  In the navigation tree dialog box, choose**OK**. The navigation tree is displayed in the left-side navigation pane.
6.  Associate datasets with the navigation tree.
    1.  In the data display area, find the target chart and click the gear icon.
    2.  In the edit dialog box,**Dataset**Area**Dimension**Select from the drop-down list**Navigation tree**Dimension, and click**OK**. The dimension of the dataset is associated with the dimension of the navigation tree.
7.  View the data presentation of the dataset.

    Select different dimension values in the navigation tree to view the corresponding data display in the data display area.

8.  In the space operation area, select**Today**,**This week**,**This month**Or manually select the start time and end time to display the data within the specified time range.

9.  After the dashboard is configured, click**Save**To save the current configuration. In addition, the system automatically saves every 10 seconds to prevent the data being edited from being lost.

    **Note:**

    -   To prevent loss of the data being edited, ARMS automatically saves the data every 10 seconds.
    -   You can adjust the chart size and position on the dashboard.
    -   Adjust the chart size

        In editing mode, you can drag the control handle in the lower right corner of a chart to adjust its size.

    -   Adjust the chart position

        In editing mode, drag the chart to adjust its position, and release the mouse to determine its final position.


