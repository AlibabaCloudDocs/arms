# Overview

Synthetic monitoring is a service that monitors performance and user experience for Internet applications such as web pages and network links.

## What is synthetic monitoring?

Synthetic monitoring provides an out-of-the-box and enterprise-level active application monitoring solution for cloud users. It utilizes global monitoring networks to manage and monitor the performance of applications in real user scenarios. You can gain a better insight into the performance of applications outside firewalls. Synthetic monitoring can explore potential failures and help improve user experience of applications.

Synthetic monitoring provides data analysis models combining multiple dimensions such as region, city, carrier, and time series, as well as rich metrics and online charts such as scattered plots and trend charts. These help you quickly discover the affected scopes and root causes of application performance problems, accurately solve IT problems, and improve service quality.

You can create browse tasks for web pages and network tasks for network links.

![yunboce_chanpingjiagou](../images/p184240.png "Architecture")

|Feature|Description|
|-------|-----------|
|Task management|Allows you to create, view, modify, and delete tasks. You can also click **Details** in the rightmost column corresponding to a task to go to the Overview page. Tasks are displayed in a list and include browse tasks and network tasks.|
|Task overview|Displays different data and charts for browse tasks and network tasks. General items include basic data such as first meaning paint, availability, downloads, as well as performance charts such as performance trend, availability, and top five slowest carriers.|
|Multidimensional reports|Allow you to analyze the performance of synthetic monitoring tasks from multiple dimensions such as map analysis, resolution analysis, trend analysis, regional analysis, and scatter analysis. You can also analyze the details of a single synthetic monitoring sample. Different metrics are displayed for browse tasks and network tasks.|

## Benefits

-   Precise and refined troubleshooting
    -   Page element errors can be detected for browse tasks and causes can be accurately located to a single network request. These can improve performance and user experience of web pages.
    -   Network tasks support DNS, Ping, and Tracert to cover multiple quality monitoring scenarios of network links.
-   Rich multidimensional analysis models

    Synthetic monitoring supports analysis models combining multiple dimensions such as region, city, and carrier. You can also analyze the details of a single sample. Rich metrics and online charts such as bar charts, line charts, scattered plots and trend charts are also provided. These help you quickly determine the affected scopes and root causes.

-   Powerful comparison of competing applications

    Without modifying application code or embed code, synthetic monitoring can not only monitor the performance of applications, but also compare the performance of competing applications. This allows you to learn about the differences from competing applications and make more competitive strategies.

-   Improved user experience

    The active solution of synthetic monitoring allows you to clearly understand the browse and network performance of applications on global terminals, and in advance locate and solve every problem that causes poor user experience.


## Scenarios

-   Monitor domain name resolution

    Synthetic monitoring checks domain name resolution time and resolution error rate to obtain detailed data of resolution processes and analyze network performance issues.

-   Monitor carriers

    Synthetic monitoring can be used to monitor carriers, obtain the performance, time, and network information of browsing for different carriers, and rank the slowest carriers.

-   Monitor user experience

    Synthetic monitoring obtains user experience in real time by monitoring web page metrics such as performance trend, error elements, and availability.

-   Compare and monitor competing applications

    Synthetic monitoring can not only monitor the performance of applications, but also compare the performance of competing applications. This allows you to learn about the differences from competing applications and make more competitive strategies.

-   Monitor page elements

    Synthetic monitoring can precisely locate element errors, display error details, and help to improve the overall display effects of web pages.


## Terms

|Term|Description|
|----|-----------|
|Browse task|A type of synthetic monitoring task. Such task monitors applications by checking URL accesses from a browser. The task supports IE full elements and Chrome full elements.|
|IE full elements|The IE browser is used to access applications.|
|Chrome full elements|The Chrome browser is used to access applications.|
|Network task|A type of synthetic monitoring task. Such task uses tools such as Ping and Tracert to monitor network health.|
|Last mile monitoring point|The monitoring point for users.|
|IDC monitoring point|The monitoring point for data centers.|
|Latency|The time for a packet or packet to be transmitted from one end of the network to the other. Latency is determined by routing conditions over the Internet. If a channel provides low speed or is too crowded, long delay or packet loss may occur.|
|Packet loss rate|The ratio of lost packets to total packets. Packet loss rate is generally caused by reasons such as physical connection failures, device failures, network congestion, and routing errors.|
|DNS query time|The time to resolve a domain name into an IP address.|
|Custom frequency|You can customize frequency parameters and the monitoring cycle.|
|Element|The text, images, audios, animations, and videos that you see when you browse web pages.|
|Error element|The element where an error occurs.|
|Error rate|The ratio of the number of errors to the number of monitoring events.|
|Carrier|Such as China Mobile, China Telecom, and China Unicom.|
|Availability|The success rate of accesses from the client that performs the monitoring task to the application.|

