# Multidimensional reports of browse tasks

You can use multidimensional reports to analyze the performance of synthetic monitoring tasks from a variety of dimensions such as the map, analysis chart, trend chart, region chart, and scatter chart.

## Prerequisites

[Create a task](/intl.en-US/Synthetic monitoring/Quick start/Create a task.md)

## Procedure

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Cloud Dial Test**.
3.  On the Scheduled dial test page, click the name of the task that you want to check or click **Details** in the rightmost column corresponding to the task.

    The Task Overview page appears.

4.  In the left-side navigation pane, click **Multidimensional Reports**.

    The Multidimensional Reports page appears. You can specify filters such as time range, domain name, and performance metrics in the section below the task name.


## Features



![Cloud dial test_map](../images/p179613.png)

-   The Map tab provides a colored map that visualizes the overall performance data of each province. Move the pointer over a province on the map to view the performance metric data of the province.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

![Cloud dial test analysis diagram](../images/p179680.png)

-   The Analysis Chart tab provides a horizontal bar chart that visualizes performance metric data of carriers. Move the pointer over a horizontal bar to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

![Cloud dial test trend graph](../images/p179681.png)

-   The Trend Chart tab provides a line chart that visualizes performance metric data of carriers. Move the pointer over a point along the line to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

![Cloud dial survey area map](../images/p179684.png)

-   The Region Chart tab provides a horizontal bar chart that visualizes performance metric data of carriers. Move the pointer over a horizontal bar to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

![Cloud dial test scatter plot](../images/p179685.png)

-   The Scatter Chart tab provides a scatter chart that visualizes performance metric data of carriers. Move the pointer over a point in the scatter chart to view the data of specific performance metrics.
-   The Statistical Data section provides the overall performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.
-   The Detailed Data section provides the detailed performance metric data of monitoring locations. For more information about metrics, see the [Metrics](#section_7yl_0t8_81a) section.

## Metrics

|Metric|Description|Performance indicator|
|Good|Moderate|Poor|
|------|-----------|---------------------|
|----|--------|----|
|Task Name|The name of the synthetic monitoring task.|N/A|
|Average Completion Time \(s\)|The average time interval between the beginning time when the page is browsed and the end time when the last packet is received in the specified time range.|≤ 10|≤ 20|\> 20|
|Availability \(%\)|The access success rate of the client that performs the monitoring task.Calculation formula: Availability = Number of effective monitoring actions/Total number of monitoring actions × 100%

|\> 96|\> 92|≤ 92|
|Average Number of Elements|The average number of loaded elements in all monitoring data.Calculation formula: Average number of elements = Total number of elements/Number of effective scatters

|≤ 80|≤ 150|\>150|
|Average Number of Error Elements|Calculation formula: Average number of error elements = Total number of error elements/Number of effective scatters|N/A|
|Number of Errors|The number of access failures during the monitoring process.|N/A|
|Number of Effective Monitoring Actions|The number of green scatters that have no error codes.|N/A|

|Data distribution|Metric|Description|Performance indicator|
|Good|Moderate|Poor|
|-----------------|------|-----------|---------------------|
|----|--------|----|
|Statistical Data|Region|The province where a monitoring carrier is located.|N/A|
|Total Downloaded Bytes \(KB\)|The average downloaded bytes for a province during the browsing process.|≤ 900|≤ 2000|\> 2000|
|Document Content Load Time \(s\)|The time interval between the beginning time when the page is browsed and the end time when documents are parsed for a specific province.|≤ 10|≤ 20|\> 20|
|Average DNS Resolution Time \(s\)|The average amount of time that is required to perform DNS resolution for all elements other than cache for a specific province.|≤ 0.15|≤ 0.3|\> 0.3|
|Average TCP Connection Time \(s\)|The average amount of time that is required to establish a TCP connection for all elements other than cache for a specific province.|≤ 0.2|≤ 0.5|\> 0.5|
|Average Download Time \(s\)|The average amount of time that is required to download all elements other than cache for a specific province.|≤ 1|≤ 2.5|\> 2.5|
|Average Response Time \(s\)|The average amount of time that is required to respond to all elements other than cache for a specific province.|≤ 0.3|≤ 0.8|\> 0.8|
|Detailed Data|City|The city in a specific province where the monitoring data is collected.|N/A|N/A|N/A|

|Data distribution|Metric|Description|
|-----------------|------|-----------|
|Statistical Data|Number of Carriers in Monitoring Locations|The total number of carriers in monitoring locations.|
|Number of Carriers in Monitored Locations|The total number of carriers whose servers are connected in monitored regions.|
|Detailed Data|Carrier in Monitoring Location|The carrier in the city where monitoring data is collected.|
|Monitored Carrier|The carrier whose data is collected.|
|Arrival Rate|Calculation formula: Arrival rate = Number of effective monitoring actions from the monitored carriers/Total number of effective monitoring actions from the carriers in the monitoring locations × 100%|

|Data distribution|Metric|Description|
|-----------------|------|-----------|
|Detailed Data|Carrier|The carrier in the city where monitoring data is collected.|

|Data distribution|Metric|Description|
|-----------------|------|-----------|
|Statistical Data|Normal Samples|The number of samples that do not contain errors during the monitoring process.|
|Application Error Samples|The number of samples that contain page loading errors.|
|Element Error Samples|The number of samples that contain element loading errors. However, the page can be normally loaded.|
|Incomplete Loading Samples|The number of samples whose visited elements are less than 80% of all elements in the specified time range.|
|Detailed Data|IP Address of Monitored Carrier|The IP address of the monitored carrier.|
|Access status|The status of the access.|

