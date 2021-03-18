# View Prometheus Monitoring metrics

The preset monitoring dashboards provided by Prometheus Monitoring show the statistics of Kubernetes clusters, Kubernetes deployment, pods, and hosts. You can view the Prometheus Monitoring metrics on these dashboards, and modify the dashboard settings such as the time range and refresh frequency to meet your business requirements.

[t855956.md\#section\_cpd\_cg9\_vul]()

## Open a monitoring dashboard

After you install the Prometheus agent, you can open the preset monitoring dashboards on the Prometheus Monitoring page.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the left-side navigation pane, click **Monitoring List**. All the Container Service for Kubernetes \(ACK\) clusters in your Alibaba Cloud account are displayed on the Prometheus Monitoring page.

4.  On the Prometheus Monitoring page, click a link in the **Installed Dashboards** column to view the monitoring dashboard in a new browser window.


## View metrics

You can view metrics on the following preset monitoring dashboards:

-   Kubernetes cluster overview dashboard

    ![K8s Cluster Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7611764161/p49438.png)

    The dashboard shows the following metrics:

    -   Total usage metrics such as Cluster CPU usage, Cluster memory usage, and Cluster filesystem usage
    -   CPU metrics such as Pods CPU usage and All processes CPU usage
    -   Memory metrics such as Pods memory usage and All processes memory usage
    -   Network metrics such as Network I/O pressure, Pods network I/O, and All processes network I/O
-   Kubernetes deployment dashboard

    ![K8s Deployment Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51317.png)

    The dashboard shows the following metrics:

    -   Deployment CPU usage, Deployment memory usage, and Unavailable Replicas in the Overview section
    -   CPU usage, Memory usage, and All processes network I/O in the Detail section
-   Pods dashboard

    ![K8s Pods Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51318.png)

    The dashboard shows the following metrics:

    -   Pod information: Pod IP Address, Pod Status, Pod Container, and Containers restarts
    -   Total usage metrics such as Pod memory usage and Pod CPU usage
    -   CPU metrics such as Pods CPU usage and All processes CPU usage
    -   Memory metrics such as Pods memory usage and All processes memory usage
    -   Network metrics such as Network I/O pressure, Pods network I/O, and All processes network I/O
-   Host details dashboard

    ![K8s Host Details Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2323672161/p49437.png)

    The dashboard shows the following metrics:

    -   CPU metrics such as CPU Cores, CPU Usage, and CPU I/O Waiting Time
    -   Memory metrics such as Total Memory and Memory Usage
    -   Disk metrics such as Total Disk Space, Disk I/O Read/Write Time, and Disk Read/Write Rate
    -   Network metrics such as Network Traffic and TCP Connections

## Common dashboard operations

The following figure shows the common operations that you can perform on the dashboards.

![common dashboard operations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51325.png)

1.  Switch dashboards

    The drop-down list shows the name of the current dashboard. You can click the down arrow to switch to another dashboard. To search for dashboards, you can enter a name in the top search bar, or select a tag from the Filter drop-down list.

    ![Switch Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51327.png)

2.  Specify the time range and refresh frequency

    After you click the clock icon, you can select a predefined time range from the drop-down panel. For example, you can select Last 5 minutes, Last 12 hours, or Last 30 days. You can also specify the start time and end time to define an absolute time range. In addition, you can set the refresh frequency for the dashboard.

    ![Set Interval and Frequency](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51326.png)

3.  Extend the time range

    Each time you click the magnifier icon, the time range is extended to twice the original length. The start time and end time are equally extended. For example, if the selected time range is Last 10 minutes and you click the magnifier icon, the start time is extended to 5 minutes earlier and the end time is extended to 5 minutes later.

4.  Manually refresh the dashboard

    Click the refresh icon to refresh the monitoring data of all panels on the current dashboard.

5.  Filter monitoring data

    Select an option from the drop-down list to filter the monitoring data displayed on the current dashboard.


## Common operations on a dashboard panel

You can click the drop-down menu at the top of a panel to perform the following operations:

![Panel Operation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5974461161/p51328.png)

-   To view the panel in the full screen mode, click **View** or press the V key. Then, you can press the V key again or press the Esc key to exit the full screen mode.
-   To share the panel, click **Share** or press the P and S keys in sequence. Then, in the Share dialog box, obtain the sharing link, embedded link, or snapshot link of the panel.
-   To obtain the JSON code of the panel, choose **More** \> **Panel JSON**, and then copy the JSON code from the JSON dialog box.
-   To export data as a CSV file from the panel, choose **More** \> **Export CSV**. In the Export CSV dialog box, configure the format in which to export the data and then export the data.
-   To enable or disable the legend, choose **More** \> **Toggle legend** or press the P and L keys in sequence.

[What is Prometheus Service?]()

[t855956.md\#section\_cpd\_cg9\_vul]()

