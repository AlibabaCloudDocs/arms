# Basic Grafana dashboards

Prometheus Service provides a variety of out-of-the-box preset Grafana dashboards. You can view Prometheus Service metrics on these dashboards, and modify the dashboard settings such as the time range and refresh frequency to meet your business requirements. This topic describes basic Grafana dashboards, including the overview dashboard, deployment dashboard, pods dashboard, and node details dashboard. This topic also describes basic operations that you can perform on these dashboards.

## Overview dashboard

![K8s Cluster Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7611764161/p49438.png)

The dashboard displays the following metrics:

-   Overall usage metrics such as Cluster CPU usage, Cluster memory usage, and Cluster filesystem usage
-   CPU metrics such as Pods CPU usage and All processes CPU usage
-   Memory metrics such as Pods memory usage and All processes memory usage
-   Network metrics such as Network I/O pressure, Pods network I/O, and All processes network I/O

## Deployment dashboard

![K8s Deployment Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51317.png)

The dashboard displays the following metrics:

-   Overview: Pod Number, spec\_replicas, Pod CPU Usage Secs, Pod Mem Used, and restarts\_total.
-   Details: Pods CPU usage, Pods memory usage, Network I/O pressure, and fs writes/reads.

## Pods dashboard

![K8s Pods Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51318.png)

The dashboard displays the following metrics:

-   Pod information such as Pod IP Address, Pod Status, Pod Container, and Container restarts
-   Overall usage metrics such as Pod CPU usage and Pod memory usage
-   CPU metrics such as Pods CPU usage and All processes CPU usage
-   Memory metrics such as Pods memory usage and All processes memory usage
-   Network metrics such as Network I/O pressure, Pods network I/O, and All processes network I/O

## Node details dashboard

![K8s Host Details Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2323672161/p49437.png)

The dashboard displays the following metrics:

-   CPU metrics such as CPU Cores, CPU Usage, and CPU I/O Waiting Time
-   Memory metrics such as Total Memory and Memory Usage
-   Disk metrics such as Total Disk Space, Disk I/O Read/Write Time, and Disk Read/Write Rate
-   Network metrics such as Network Traffic and TCP Connections

## Basic operations on Grafana dashboards

**Note:** This section describes only basic operations on Grafana dashboards. For more information about advanced operations, see [Grafana documentation](https://grafana.com/docs/grafana/latest/).

You can perform the following basic operations on Grafana dashboards.

**Switch between dashboards**

1.  At the top of the Grafana page, click the name of the current dashboard.

    ![Grafana - switch between dashboards 01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2238015261/p268532.png)

2.  Enter a dashboard name in the top search box, or click Filter by tag in the upper-right corner and select a tag to display dashboards to which the tag is attached.

    ![Switch Dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51327.png)

3.  Click the name of the dashboard that you want to view.

**Set the time range and refresh frequency**

1.  In the upper-right corner of the Grafana page, click the box for setting the time range.

    ![Basic operations on Grafana dashboards](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7365980261/p51325.png)

2.  Select a predefined relative time range for monitoring data from the drop-down panel. For example, you can select Last 5 minutes, Last 12 hours, or Last 30 days. You can also set the start time and end time to define an absolute time range.

    ![Set Interval and Frequency](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8611764161/p51326.png)


**Extend the time range**

In the upper-right corner of the Grafana page, click the ![Grafana - extend the time range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3238015261/p268559.png) icon.

Each time you click the Magnifier icon, the time range is extended to twice the original length. The start time and end time are equally extended. For example, if the selected time range is Last 10 minutes and you click the magnifier icon, the start time is extended to 5 minutes earlier and the end time is extended to 5 minutes later.

![Grafana - extend the time range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3238015261/p268552.png)

**Manually refresh the dashboard**

In the upper-right corner of the Grafana page, click the ![Grafana - refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3238015261/p268561.png) icon to refresh the monitoring data of all panels on the current dashboard.

![Grafana - refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3238015261/p268554.png)

**Filter monitoring data**

On the Grafana page, select an option from the drop-down list to filter the monitoring data that is displayed on the current dashboard, as shown in the following figure.

![Grafana - filter monitoring data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3238015261/p268557.png)

## Basic operations on dashboard panels

You can click the drop-down menu at the top of a panel and select an option to perform basic operations on the panel.

![Panel Operation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7365980261/p51328.png)

-   To view the panel in full screen mode, click **View** or press the V key. You can press the V key again or press the Esc key to exit the full screen mode.
-   To edit the panel, click **Edit** or press the E key. On the Edit Panel page, modify information about the panel and click **Apply** in the upper-right corner.
-   To share the panel, click **Share** or press the P and S keys in sequence. In the Share Panel dialog box, obtain the sharing link, embedded link, or snapshot link of the panel.
-   To explore the panel, click **Explore** or press the X key. On the Explore page, check metrics, troubleshoot issues, or explore data.
-   To export the data of the panel as a CSV file, choose **Inspect** \> **Data**. On the Data tab, click **Download CSV** to export data.
-   To view the query metrics of the panel, choose **Inspect** \> **Query**. On the Query tab, view the request and response.
-   To obtain the JSON code of the panel, choose **Inspect** \> **Panel JSON**. On the JSON tab, copy the JSON code.
-   To copy and paste the panel, choose **More** \> **Duplicate**, or press the P and D keys in sequence. The panel is copied and pasted into the current dashboard.
-   To copy the panel, choose **More** \> **Copy**. The panel is copied.

