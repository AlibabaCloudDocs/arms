# Overview of network tasks

After a synthetic monitoring network task is created, you can view the overall performance of the network task on the Task Overview page.

## Prerequisites

[Create a task]()

## Procedure

1.  In the left-side navigation pane, click **Synthetic Monitoring**.
2.  On the Scheduled Synthetic Monitoring page, find a task and click the name of the task or **Details** in the rightmost column.

    The Task Overview page appears. You can select a time range in the upper part of the page.

    ![Network task overview](../images/p182201.png)


## Metrics

-   The following table describes the metrics in the Basic Data section.

    |Metric|Description|Threshold|
|Good|Fair|Poor|
    |------|-----------|---------|
    |----|----|----|
    |Latency|The time for a packet or packet to be transmitted from one end of the network to the other.|≤ 40|≤ 100|\>100|
    |Packet loss rate|Packet loss rate = Lost packets/Total transmitted packets × 100%|≤ 5|≤ 10|\>10|
    |DNS query time|The time to resolve a domain name into an IP address.|≤ 0.08|≤ 0.15|\>0.15|
    |Resolution error rate|The error rate during the domain name resolution.Resolution error rate = Resolution errors/Total resolved domain names × 100%

|≤ 3|≤ 5|\>5|
    |Alerting|Expected to be available|None|None|None|

-   Performance trend: indicates the changes of latency over a period.
-   Availability: indicates the changes of packet loss rate over a period.
-   Top 5 carriers by Latency: displays the five carriers that have the longest latency in task execution.
-   Top 5 Error Types: displays the five error types that occur most frequently in job execution. You can also view the specific error codes and the number of errors.
-   The Details of Synthetic Monitoring Points section displays detailed data of all synthetic monitoring points. The following table describes the metric in this section.

    You can click the row of a carrier in a city to view the detailed synthetic monitoring information. For more information, see [Synthetic Monitoring Details](#section_e61_zv3_9c0).

    |Metric|Description|Threshold|
|Good|Fair|Poor|
    |------|-----------|---------|
    |----|----|----|
    |Latency \(ms\)|The time for a packet or packet to be transmitted from one end of the network to the other.|≤ 40|≤ 100|\>100|
    |DNS query time \(s\)|The time to resolve a domain name into an IP address.|≤ 0.08|≤ 0.15|\>0.15|
    |Resolution error rate \(%\)|The error rate during the domain name resolution.Resolution error rate = Resolution errors/Total resolved domain names × 100%

|≤ 3|≤ 5|\>5|
    |Packet loss rate \(%\)|Packet loss rate = Lost packets/Total transmitted packets × 100%|≤ 5|≤ 10|\>10|
    |Tracert latency \(ms\)|The average latency of all hops during the Tracert process.|≤ 40|≤ 100|\>100|
    |Tracert hops|The number of network devices involved in the Tracert process.|≤ 15|≤ 25|\>25|


## Synthetic Monitoring Details



On the Synthetic Monitoring Details page, you can view the basic information, network information, DNS request analysis, Ping monitoring analysis, and Tracert monitoring analysis of a carrier.

![dns request analysis](../images/p182209.png)

You can view the following parameters in the DNS request analysis section:

-   A record: specifies the IP address record mapped to the host name \(or domain name\).
-   CNAME record: allows multiple domain names to be mapped to the same IP address.
-   DNS query time: the time to resolve a domain name into an IP address.
-   DNS tracing: records the process where DNS resolves and traces a domain name.

The PING monitoring analysis area displays the process analysis for pinging target IP addresses.

![PING monitoring analysis](../images/p182211.png)

The TRACERT monitoring analysis area displays the IP address and time used during the Tracert tracing process.

![TRACERT monitoring analysis](../images/p182212.png)

