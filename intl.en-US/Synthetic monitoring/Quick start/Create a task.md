# Create a task

The Synthetic Monitoring module allows you to create browse tasks and network tasks. If you want to use the Synthetic Monitoring module to test your application, you must create a synthetic monitoring task first.

The Synthetic Monitoring module uses the globally distributed monitoring networks to view and perform network synthetic monitoring on web applications such as websites and servers.

## Procedure

1.  In the left-side navigation pane, choose **Synthetic Monitoring**. On the Scheduled Synthetic Monitoring page, click **Create a scheduled task** in the upper-right corner.

2.  In the Basic Information step, set Task Name, Task Address, and Task Type, and then click **Next**.

    -   To create a browse task, set Task Type to Browse - IE Full Elements or Browse - Chrome Full Elements \(HTTP 1.1/2.0\).
    -   To create a network task, set Task Type to Network.
3.  In the Monitoring Points step, add monitoring points and then click **Next**.

    Set **Adding Method** to Recommended Monitoring Point Group or Custom, select one or more groups in the left list, click ![right_arrow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9595758061/p179404.png) to add the groups to the right Added list. You can add up to 50 monitoring points for a task. If you add more than 50 monitoring points, only the first 50 monitoring points are valid.

4.  In the Monitoring Parameters step, configure the parameters and then click **Next**.

    A browse task have different monitoring parameters from those of a network task.

    |Parameter|Description|
    |---------|-----------|
    |IP Address Type|The type of the IP address. Valid values:    -   Automatic
    -   IPv4
    -   IPv6 |
    |Associated Items|The associated items of monitoring. Valid values:    -   Disable Caching: indicates whether cached resources can be loaded when the page is loaded.
    -   Return Elements: indicates whether to return the elements of the page.
    -   Redirection: indicates whether to continue browsing after a redirection occurs.
    -   Disable Compression: uses the Accept-Encoding field to determine whether to accept compressed files.
    -   Automatic Scrolling: indicates whether to automatically scroll up and down the screen and load the page.
    -   Ignore Certificate Errors: indicates whether to ignore certificate errors during certificate verification in the SSL Handshake and continue browsing.
    -   Filter Out Invalid IP Address: indicates whether to filter out the invalid IP address, which is 127.0.0.1. |
    |QUIC Version|Select the QUIC version.|
    |QUIC Request Element Domain|The domain name of the QUIC request element.|
    |Advanced Settings|
    |Return Request Header|The type of the returned request header. Valid values:    -   Return Basic Document: The HTML request header of the page is returned.
    -   Return All Elements: All element resources of the page are returned.
    -   None |
    |Return Response Header|The type of the returned response header. Valid values:    -   Return Basic Document: The HTML response header of the page is returned.
    -   Return All Elements: All element resources of the page are returned.
    -   None |
    |Environment ID|The ID of the environment. When the monitoring point does not meet the Framework version requirements defined when the task is created, an error is reported. Valid values:

    -   Framework 2.0
    -   Framework 3.0
    -   Framework 3.5
    -   Framework 4.0
    -   Framework 4.5 |
    |Custom Host|The custom host mode. Valid values:    -   Round Robin
    -   Random
The custom host mode can contain multiple IP addresses. Separate multiple IP addresses with commas \(,\). Example: ipv4:192.168.2.1,192.168.2.5:img.a.com\|192.168.2.1\[8080\]:img.a.com.

**Note:** If a colon \(:\) occurs, a URL before the colon \(:\) is automatically resolved. |
    |Custom Header|Allows you to add or modify some field values in the request header. Valid values:    -   Modify First Packet: modifies the header of only the packet sent in the first request for the browse task.
    -   Modify All Packets: modifies the headers of all packets.
    -   Off: The header of a packet is not modified.
Custom Host Format: You can add multiple fields. Separate multiple fields with vertical bars \(\|\). Example: Host:www.example.com\|Referer:www.example.com.|
    |Element Blacklist|An element added in the element blacklist will not be loaded in the page loading process.|
    |Element Whitelist|The elements in the element whitelist must be included in the element blacklist. An element added in the element whitelist will be loaded in the page loading process.|
    |Process ID|Indicates whether the task manager on the host that executes the task contains the process name. If not, an error will be reported.|
    |First Screen ID|If this parameter is selected and the specified URL is loaded in the page loading process, ARMS reckons that the first screen is loaded.|
    |Verification String Blacklist|If the source code returned by the client contains any of the specified strings, an error is returned. Separate multiple strings with vertical bars \(\|\).|
    |Verification String Whitelist|If the source code returned by the client does not contain any of the specified strings, an error is returned. Separate multiple strings with vertical bars \(\|\).|
    |Monitoring Timeout|The default value is 40 seconds. After the onload event, ARMS periodically checks the working status of the browser. If the browser is busy, ARMS continues to wait. If the browser status remains busy till the timeout vlaue is reached, the task is stopped and data is reclaimed. If the browser is idle, ARMS stops checking its working status.|
    |Waiting Period|The default waiting period is 3.8 seconds. ARMS checks the working status of the browser of time once within each waiting period.|
    |Start Execution Time|The time when monitoring starts. It is valid for low-frequency tasks. The start time cannot be greater than the task frequency.|
    |Evenly Distribute Monitoring Samples|Offset = Number of minutes/Number of carriers. The earliest delivery time of each carrier is the start execution time plus the offset.|

    |Parameter|Valid value|Description|
    |---------|-----------|-----------|
    |IP Address Type|N/A|The type of the IP address. Valid values:    -   Automatic
    -   IPv4
    -   IPv6 |
    |Filter Out Invalid IP Address|N/A|Indicates whether to filter out the invalid IP address, which is 127.0.0.1.|
    |DNS Monitoring|Monitoring Timeout|The default value is 5 seconds. A timeout event is returned when the specified value is reached.|
    |Query Method|The query method. Valid values:    -   Recursion: normal DNS query
    -   Iteration: queries records on the authoritative DNS server. |
    |NS Server|You can specify a DNS server.|
    |DIG|Indicates whether to display the data in the DIG format.|
    |DNS Server Type|The type of the DNS server. Valid values:    -   Automatic
    -   IPv4
    -   IPv6 |
    |Tracert Monitoring|Monitoring Timeout|The default value is 60 seconds. If the preset value is reached, ARMS reckons that the server is unreachable and the task is terminated.|
    |Maximum Hops|The maximum number of hops allowed in route tracing. The default value is 20. If the preset value is reached, ARMS reckons that the server is unreachable.|
    |Ping Monitoring|Protocol type|The type of the protocol. Valid values:    -   ICMP
    -   TCP |
    |Monitoring Timeout|The default value is 20 seconds. If the preset value is reached, the Ping operation fails.|
    |Execution Interval|The next Ping packet is sent in the specified time after the Ping response data is received for the previous packet.|
    |Split Package|After you select this parameter, you can customize the number and size of packets.|
    |Packages|The number of packets. The default value is 4.|
    |Package Size|The size of the packet.|
    |Start Execution Time|N/A|The time when monitoring starts. It is valid for low-frequency tasks. The start time cannot be greater than the task frequency.|
    |Evenly Distribute Monitoring Samples|N/A|Offset = Number of minutes/Number of carriers. The earliest delivery time of each carrier is the start execution time plus the offset.|

5.  In the Monitoring Cycle step, set Monitoring Cycle and Monitoring Frequency, and then click **Next**.

6.  In the Preview & Publish step, confirm the parameters and click **Complete**.

    Then, you are redirected to the Scheduled Synthetic Monitoring page.


## References

On the Scheduled Synthetic Monitoring page, you can view the task name, task type, URL, number of monitoring points, creation time, availability, and task status of a synthetic monitoring task.

-   Find the task and click the name of the task or **Details** in the rightmost column to go the Task Overview page.
-   Click **Edit** in the rightmost column to modify the task.
-   Click **Enable** in the rightmost column to enable the task.
-   Click **Disable** in the rightmost column to disable the task.
-   Click **Delete** in the rightmost column to delete the task.

