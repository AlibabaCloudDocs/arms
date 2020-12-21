# Overview of browse tasks

After you create a scheduled browse task, you can view the overall performance of the task on the Task Overview page.

## Prerequisites

[Create a task]()

## Procedure

1.  In the left-side navigation pane, click **Cloud Dial Test**.
2.  On the Scheduled dial test page, click the name of the task that you want to check or click **Details** in the rightmost column corresponding to the task.

    The Task Overview page appears. You can specify a time range in the section below the task name.

    ![Task overview](../images/p179521.png)


## Metrics

-   The following table describes the metrics that are provided in the Basic Metrics section.

    |Metric|Description|Performance indicator|
|Good|Moderate|Poor|
    |------|-----------|---------------------|
    |----|--------|----|
    |100 KB Load Time|The average amount of time that is required to load 100 KB data. Unit: seconds.Calculation formula: 100 KB load time = Average completion time/Total downloaded bytes × 100

|≤ 0.5|≤ 1|\> 1|
    |First Page Load Time|The time interval between the time when the URL request is issued and the time when the rendered height of the page is greater than or equal to the specified height.The default height is 600 pixels. You can customize the height. Unit: seconds.

|≤ 3.5|≤ 7|\> 7|
    |Availability|The access success rate of the client that performs the monitoring task.Calculation formula: Availability = Number of effective monitoring actions/Total number of monitoring actions × 100%

**Note:** Green scatters that have no errors indicate effective monitoring actions. All scatters indicate the total number of monitoring actions.

|\> 96|\> 92|≤ 92|
    |Downloaded Bytes|The average bytes of downloaded data. Unit: KB.Calculation formula: Download bytes = Total downloaded bytes of effective scatters/Number of effective scatters

|≤ 900|≤ 2000|\> 2000|
    |Alerts|This metric will be available in the future.|N/A|N/A|N/A|

-   Performance trend: the line chart of the Average Completion Time metric. The line chart visualizes the time interval between the beginning time when the page is browsed and the end time when the last packet is received in the specified time range. Unit: seconds.
-   Availability: the line chart that visualizes the access success rate of the client that performs the monitoring task.
-   Top 5 Slow Carriers: the vertical bar chart that visualizes the top five carriers that have the highest latency in task execution. The vertical bar chart is based on the average value of the Average Completion Time metric values of all scatters for each carrier in the specified time range.
-   Top 5 Error Types: the vertical bar chart that visualizes the top five error types that are repeated most frequently in task execution. The vertical bar chart is based on the five scatters that contain the largest number of errors in the specified time range.
-   Domain Name Query Time Proportion: the horizontal stacked bar chart that visualizes the query time proportions of domain names.
-   Time Proportion: the horizontal stacked bar chart that visualizes the time proportions of the DNS Resolution Time, TCP Connection Time, Response Time, and Download Time metrics.

    Calculation method: Calculate the average value of each metric. Then, calculate the time proportion of each average value to the total average values of the four metrics.

    |Metric|Description|Performance indicator|
|Good|Moderate|Poor|
    |------|-----------|---------------------|
    |----|--------|----|
    |DNS Resolution Time|The total amount of time that is required to perform DNS resolution for all elements. The overlapping time is counted only once and the time intervals between DNS resolutions are ignored. Unit: seconds.|≤ 0.8|≤ 1.8|\> 1.8|
    |TCP Connection Time|The total amount of time that is required to establish a TCP connection for all elements. The overlapping time is counted only once and the time intervals between TCP connections are ignored. Unit: seconds.|≤ 1.5|≤ 2.5|\> 2.5|
    |Response Time|The total amount of time that is required to respond to all elements. The overlapping time is counted only once and the time intervals between responses are ignored. Unit: seconds.|≤ 3.5|≤ 8|\> 8|
    |Download Time|The total amount of time that is required to download all elements. The overlapping time is counted only once and the time intervals between downloads are ignored. Unit: seconds.|≤ 6|≤ 12|\>12|

-   The following list describes the metrics in the Synthetic Peer Summary section.

    To view the synthetic monitoring details of a carrier for the browse task, click anywhere in the row corresponding to a carrier. For more information, see the [Synthetic peer details](#section_lku_4tb_c45) section of this topic.

    -   Average Completion Time \(s\): the time interval between the beginning time when the page is browsed and the end time when the last packet is received. Unit: seconds.
    -   Total Downloaded Bytes \(KB\): the average downloaded bytes during the browsing process.
    -   Document Content Load Time \(s\): the time interval between the beginning time when the page is browsed and the end time when documents are parsed. Unit: seconds.
    -   Average DNS Resolution Time \(s\): the average amount of time that is required to perform DNS resolution for all elements other than cache.
    -   Average TCP Connection Time \(s\): the average time that is required to establish a TCP connection for all elements other than cache.
    -   Average Response Time \(s\): the average amount of time that is required to respond to all elements other than cache.
    -   Average Download Time \(s\): the average amount of time that is required to download all elements other than cache.
    -   Average Number of Elements: the average number of elements that are loaded in all monitoring data. Calculation formula: Average number of elements = Total number of all elements/Number of effective scatters
    -   Average Number of Error Elements: the average number of error elements. Calculation formula: Average number of error elements = Total number of error elements/Number of effective scatters

## Synthetic peer details

In the Synthetic Peer Details panel, you can view the basic information, network information, system environment, resource usage, all elements, and visualized reports of a carrier.

![Browse dial test details](../images/p179963.png)

The following table describes the metrics in the All Elements section.

|Category|Metric|Description|Performance indicator|
|Good|Moderate|Poor|
|--------|------|-----------|---------------------|
|----|--------|----|
|Complete Load|Average Completion Time|The time interval between the beginning time when the page is browsed and the end time when the last packet is received. Unit: seconds.|≤ 10|≤ 20|\> 20|
|First Page Load Time|The time interval between the time when the URL request is issued and the time when the rendered height of the page is greater than or equal to the specified height. The default height is 600 pixels. You can customize the height. Unit: seconds.|≤ 3.5|≤ 7|\> 7|
|Visually Complete Time|The time when all elements in the specified height of the page are rendered for the first time. The default page height is 600 pixels. You can specify the height based on the URL of the first page. Unit: seconds.|≤ 6|≤ 12|\> 12|
|Time To First Byte|The time interval between the beginning time when the page is browsed and the time when the first packet is received. Unit: seconds.Calculation formula: Time to first byte = DNS response time + TCP connection time + \(SSL handshake time\) + Request time + Response time

|N/A|N/A|N/A|
|Document Content Load Time|The time interval between the beginning time when the page is browsed and the end time when documents are parsed. Unit: seconds.|≤ 10|≤ 20|\> 20|
|Document Load|DNS Resolution Time|The amount of time that is required to perform DNS resolution for documents. Unit: seconds.|≤ 0.1|≤ 0.2|\> 0.2|
|Document TCP Connection Time|The amount of time that is required to establish a TCP connection for documents. Unit: seconds.|≤ 0.12|≤ 0.25|\> 0.25|
|Document SSL Handshake Time|The amount of time that is required to perform SSL handshakes to download documents. Unit: seconds.|≤ 0.5|≤ 1|\> 1|
|Document Request Time|The amount of time that is required to receive requests to download documents. Unit: seconds.|N/A|N/A|N/A|
|Document Response Time|The amount of time that is required to respond to documents. Unit: seconds.|≤ 0.3|≤ 0.8|\> 0.8|
|Document Download Time|The amount of time that is required to download documents. Unit: seconds.|≤ 1|≤ 2.5|\> 2.5|
|Others|Redirect Time|The amount of time that is required to follow redirections in responses before documents are downloaded during the browsing process. Unit: seconds.|N/A|N/A|N/A|
|Resource Download Time|The amount of time that is required to download elements other than documents. Unit: seconds.Calculation formula: Resource download time = Average completion time - Document download time

|N/A|N/A|N/A|
|Page Load Speed|The average speed at which the page is loaded. Unit: bytes per second.Calculation formula: Page load speed = Total downloaded bytes/Average completion time

|\> 150|\> 80|≤ 80|
|Document Load Speed|Unit: bytes per second. Calculation formula: Document load speed = Document downloaded bytes/Document download time|\> 220|\> 100|≤ 100|
|Other Element Rendering Speed|The speed at which elements other than documents are loaded and rendered after documents are downloaded. Unit: bytes per second.Calculation formula: Other element rendering bytes = Total downloaded bytes - Document downloaded bytes

Other element rendering time = Average completion time - Document download time

Other element rendering speed = Other element rendering bytes/Other element rendering time

|\> 180|\> 100|≤ 100|
|Network Round Trips|The number of requests to network resources.|≤ 80|≤ 150|\> 150|
|Number of DNS Resolutions|The total number of DNS resolutions during the browsing process.|≤ 30|≤ 50|\> 50|
|Number of TCP Connections|The total number of TCP connections during the browsing process.|≤ 50|≤ 90|\> 90|
|IP Address of Monitored Carrier|The IP address of the monitored carrier.|N/A|N/A|N/A|
|Total Downloaded Bytes|The total bytes that are downloaded during the browsing process.|N/A|N/A|N/A|
|Document Downloaded Bytes|The total bytes of HTML documents on the browsed page.|N/A|N/A|N/A|

In the Visualized Reports section, you can view [Element Domain Name Pie Chart](#section_vow_s8y_h52) and [Element Type Pie Chart](#section_8fr_bju_crq).

## Element Domain Name Pie Chart

On the Element Domain Name Pie Chart page, you can view the basic information, network information, system environment, resource usage, performance distribution, throughput distribution, and domain name list of a carrier.

![Element Domain Pie Chart](../images/p179985.png)

-   Performance distribution: the pie chart that visualizes the proportions of loading time for the pages corresponding to domain names. Labels outside pie slices describe domain names and proportions. You can also move the pointer over a slice to view a domain name and a proportion. Below the pie chart, the legend section annotates domain names in different colors. Each legend is linked to a slice. You can click a legend to hide or show a slice that represents a domain name. If a slice is hidden, the legend that is linked to the slice is displayed in gray.
-   Throughput distribution: the pie chart that visualizes the proportions of throughput for the pages corresponding to domain names. Labels outside pie slices describe domain names and proportions. You can also move the pointer over a slice to view a domain name and a proportion. Below the pie chart, the legend section annotates domain names in different colors. Each legend is linked to a slice. You can click a legend to hide or show a slice that represents a domain name. If a slice is hidden, the legend that is linked to the slice is displayed in gray.
-   Domain name list: the list that describes the details of domain names. The following table describes the metrics in the list.

    |Metric|Description|
    |------|-----------|
    |Domain Name|The domain name.|
    |Average Completion Time \(s\)|The average time interval between the beginning time when the page is browsed and the end time when the last packet is received. Unit: seconds.|
    |Total Downloaded Bytes \(KB\)|The total bytes that are downloaded during the browsing process. Unit: KB.|
    |Number of Elements|The number of elements of a domain name.|
    |Number of Error Elements|The total number of error elements of a domain name.|
    |Element Availability \(%\)|Calculation formula: Element availability = Number of loaded elements/Total number of elements|
    |CNAME|The CNAME record that maps multiple domain names to a single URL. The CNAME record must be placed before a colon \(:\), and the URL must be placed after the colon \(:\).|


## Element Type Pie Chart

On the Element Type Pie Chart page, you can view the basic information, network information, system environment, resource usage, performance distribution, throughput distribution, and element type list of a carrier.

![Element type pie chart](../images/p179989.png)

-   Performance distribution: the pie chart that visualizes the proportions of loading time for the elements of different types. Labels outside pie slices describe element types and proportions. You can also move the pointer over a slice to view the corresponding element type and proportion. Below the pie chart, the legend section annotates element types in different colors. Each legend is linked to a slice. You can click a legend to hide or show a slice that represents an element type. If a slice is hidden, the legend that is linked to the slice is displayed in gray.
-   Throughput distribution: the pie chart that visualizes the proportions of throughput for the elements of different types. Labels outside pie slices describe element types and proportions. You can also move the pointer over a slice to view the corresponding element type and proportion. Below the pie chart, the legend section annotates element types in different colors. Each legend is linked to a slice. You can click a legend to hide or show a slice that represents an element type. If a slice is hidden, the legend that is linked to the slice is displayed in gray.
-   Element type list: the list that describes the details of element types. The following table describes the metrics in the list.

    |Metric|Description|
    |------|-----------|
    |Element Type|The type of the element.|
    |Average Completion Time \(s\)|The average time interval between the beginning time when the page is browsed and the end time when the last packet is received. Unit: seconds.|
    |Total Downloaded Bytes \(KB\)|The total bytes that are downloaded during the browsing process. Unit: KB.|
    |Number of Elements|The number of elements of a type.|
    |Number of Error Elements|The total number of error elements of a type.|
    |Element Availability \(%\)|Calculation formula: Element availability = Number of loaded elements/Total number of elements|


