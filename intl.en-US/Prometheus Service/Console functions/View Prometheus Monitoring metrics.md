# View Prometheus Monitoring metrics

The preset monitoring dashboards provided by Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) contain the Kubernetes cluster overview, Kubernetes deployment, pods, and host details. You can view a wide range of Prometheus metrics through these dashboards, and modify the attributes such as the time range and refresh frequency of the dashboard data as needed.

[t855956.md\#section\_cpd\_cg9\_vul]()

## Open a monitoring dashboard

After installing the Prometheus agent, you can open the preset monitoring dashboards on the Prometheus monitoring page.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

    On the Prometheus monitoring page, all the Container Service Kubernetes clusters under your Alibaba Cloud account are displayed.

3.  On the Prometheus monitoring page, click a link in the **Has installation plugins** column to access the monitoring dashboard in a new browser window.


## View monitoring metrics

You can view monitoring metrics on the following preset monitoring dashboards:

-   Kubernetes cluster overview dashboard

    The dashboard displays the following monitoring metrics:

    -   Total Usage: Cluster CPU Usage, Cluster Memory Usage, and Cluster Filesystem Usage
    -   CPU Usage: Pod CPU Usage and Processes CPU Usage
    -   Memory Usage: Pod Memory Usage and Processes Memory Usage
    -   Network Info: Network I/O Pressure, Pod Network I/O, and Processes Network I/O
-   Kubernetes deployment dashboard

    The dashboard displays the following monitoring metrics:

    -   Overview: Deployment CPU usage, Deployment Memory Usage, and Unavailable Replicas
    -   Detail: CPU Usage, Memory Usage, and Processes Network I/O
-   Pod dashboard

    The dashboard displays the following monitoring metrics:

    -   Pod Info: Pod IP Address, Pod Status, Pod Container, and Container restarts
    -   Total Usage: Pod Memory Usage and Pod CPU Usage
    -   CPU Usage: Pod CPU Usage and Processes CPU Usage
    -   Memory Usage: Pod Memory Usage and Processes Memory Usage
    -   Network Info: Network I/O Pressure, Pod Network I/O, and Processes Network I/O
-   Host details dashboard

    The dashboard displays the following monitoring metrics:

    -   CPU Info: CPU Cores, CPU Usage, and CPU Iowait
    -   Memory Info: Total Memory and Memory Usage
    -   Disk Info: Total Disk Space, Disk I/O Read/Write Time, and Disk Read/Write Rate
    -   Network Info: Network Traffic and TCP Connections

## Common operations on dashboards

The following figure shows the common operations on dashboards.

1.  Switch dashboards

    The drop-down list displays the name of the currently viewed dashboard and can be used to switch to another dashboard. You can enter a name in the search bar on the top to search for a dashboard, or use Filter to search for a dashboard with a specified tag from the drop-down list.

2.  Set the time interval and refresh frequency

    After clicking the icon, you can select a predefined time interval for monitoring data, such as the last 5 minutes, last 12 hours, or last 30 days. You can also customize an absolute time interval by setting the start time and end time. In addition, you can set the dashboard refresh frequency.

3.  Expand the time interval

    When you click the expand button each time, the time interval is expanded twice, with the start time earlier and end time later equally. Assume that the selected time interval is the last 10 minutes. After you click the button, the start time is 5 minutes earlier while the end time is 5 minutes later.

4.  Manually refresh the dashboard

    Click this button to refresh the monitoring data of all panels on the current dashboard.

5.  Filter monitoring data

    Select an option from the drop-down list to filter the monitoring data displayed on the current dashboard.


## Common operations on the dashboard panel

Click the drop-down menu at the top of the panel to perform the following operations:

-   View the current panel in full screen: Click **View** or press the shortcut key V. Press the shortcut key V again or press Esc to exit the full screen.
-   Share the current panel: Click **Share** or press P and S in sequence to access the Share dialog box and acquire the sharing link, embedded link, or snapshot link of the current panel.
-   Acquire the JSON code of the current panel: Choose **More** \> **Panel JSON** and then copy the JSON code in the JSON dialog box.
-   Export data on the current panel into a CSV file: Choose **More** \> **Export CSV**. In the Export CSV dialog box, set the format and export the file.
-   Toggle legends: Choose **More** \> **Toggle legend** or press P and L in sequence to toggle the legends.

[What is Prometheus Service?]()

[t855956.md\#section\_cpd\_cg9\_vul]()

