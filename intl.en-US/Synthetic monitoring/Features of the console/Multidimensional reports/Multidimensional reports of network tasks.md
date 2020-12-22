# Multidimensional reports of network tasks

You can use multidimensional reports to analyze the performance of synthetic monitoring tasks from a variety of dimensions such as the map, analysis chart, trend chart, region chart, and scatter chart.

## Prerequisites

[Create a task](/intl.en-US/Synthetic monitoring/Quick start/Create a task.md)

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Cloud Dial Test**.
3.  On the Scheduled dial test page, click the name of the task that you want to check or click **Details** in the rightmost column corresponding to the task.

    The Task Overview page appears.

4.  In the left-side navigation pane, click **Multidimensional Reports**.

    The Multidimensional Reports page appears. You can specify filters such as time range and performance metrics in the section below the task name.


## Introduction



-   The Map tab provides a colored map that visualizes the overall performance data of each province. Move the pointer over a province on the map to view the performance metric data of the province.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

-   The Analysis Chart tab provides a horizontal bar chart that visualizes performance metric data of carriers. Move the pointer over a horizontal bar to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

-   The Trend Chart tab provides a line chart that visualizes performance metric data of carriers. Move the pointer over a point along the line to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

-   The Region Chart tab provides a horizontal bar chart that visualizes performance metric data of carriers. Move the pointer over a horizontal bar to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

-   The Scatter Chart tab provides a scatter chart that visualizes performance metric data of carriers. Move the pointer over a point in the scatter chart to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

## Metrics

|Metric|Description|Performance indicator|
|Good|Moderate|Poor|
|------|-----------|---------------------|
|----|--------|----|
|Task Name|The name of the synthetic monitoring task.|N/A|
|Region|The region where the task node is located.|N/A|
|Latency \(ms\)|The time required for a message or a packet to be transmitted from one end to another.|≤ 40|≤ 100|\>100|
|DNS Query Time \(s\)|The time required to resolve a domain name into an IP address.|≤ 0.08|≤ 0.15|\>0.15|
|Resolution Error Rate \(%\)|The percentage of resolutions that have errors taking up the total resolutions.Resolution error rate \(%\) = Number of resolutions that have errors/Total number of resolutions × 100%

|≤ 3|≤ 5|\>5|
|Packet Loss Rate \(%\)|Packet loss rate \(%\) = Number of lost packets/Total number of transmitted packets × 100%.|≤ 5|≤ 10|\>10|
|Tracert Latency \(ms\)|The average latency of all hops in the Tracert process.|≤ 40|≤ 100|\>100|
|Tracert Hops|The number of network devices involved in the Tracert process.|≤ 15|≤ 25|\>25|
|Failures|The number of access failures in the monitoring process.|N/A|N/A|N/A|
|Number of Effective Monitoring Actions|The number of green scatters that have no error codes.|N/A|N/A|N/A|
|Number of Carriers in Monitoring Locations|The total number of carriers in monitoring locations.|N/A|N/A|N/A|
|Number of Carriers in Monitored Locations|The total number of carriers whose servers are connected in monitored regions.|N/A|N/A|N/A|

|Data distribution|Metric|Description|
|-----------------|------|-----------|
|Detailed data|Arrival Rate|Arrival rate = Number of effective monitoring actions from the monitored carriers/Total number of effective monitoring actions from the carriers in the monitoring locations × 100%|

|Data distribution|Metric|Description|
|-----------------|------|-----------|
|Statistical data|Total Samples|The total number of samples.|
|Normal Samples|The number of samples that do not have exceptions in the monitoring process.|
|Application Error Samples|The number of samples that contain page loading errors.|
|Detailed data|IP Address of Monitored Carrier|The IP address of the monitored carrier.|
|Access Status|The status of the access.|

