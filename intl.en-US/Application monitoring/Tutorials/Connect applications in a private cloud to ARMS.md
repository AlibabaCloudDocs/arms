# Connect applications in a private cloud to ARMS

This topic shows you how to use Gateway to connect applications in a private cloud to Application Real-Time Monitoring Service \(ARMS\) on Alibaba Cloud.

## Scenario

ARMS on Alibaba Cloud cannot directly monitor applications in a private cloud due to a network connection issue. In this case, you can deploy Gateway on the classic network or a virtual private cloud \(VPC\) of Alibaba Cloud and use Gateway as a proxy to connect the applications to ARMS.

## Deployment principle

1.  ARMS Gateway cluster A deployed in the DMZ exposes the internal endpoint to Apsara Stack and the private cloud. The ARMS agents deployed in Apsara Stack and WebLogic send the collected monitoring data to the Gateway cluster.
2.  The DMZ is connected to Alibaba Cloud by using a leased line. ARMS Gateway cluster B deployed in a VPC on Alibaba Cloud is connected to ARMS Gateway cluster A by using the leased line and acts as a bridge.
3.  ARMS Gateway cluster B sends the collected monitoring data to the ARMS server on Alibaba Cloud.
4.  ARMS agents installed on Alibaba Cloud, including frontend agents deployed on pages, send data to the ARMS server on Alibaba Cloud.

## Requirements on hybrid cloud deployment of ARMS

-   Assume that you need to collect data from 500 nodes in Apsara Stack and the private cloud. You must prepare six virtual machines to deploy two Gateway clusters. Each virtual machine is allocated 2 CPU cores and 8 GB memory. Each Gateway cluster contains three virtual machines on which Gateway is deployed.
-   The monitoring data that is sent from Gateway to Alibaba Cloud is small in size and occupies less than 1 Mbit/s bandwidth. You can use the bandwidth of the existing leased line and install ARMS agents in Enterprise Distributed Application Service \(EDAS\) of Apsara Stack and WebLogic to monitor applications, without the need to modify application code.

## Connect an application to ARMS

1.  Download the [Gateway package](https://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-gateway-1.7.0.jar). In this example, Gateway connects to the ARMS service in the China \(Hangzhou\) region.
2.  Deploy Gateway on a proxy server and run the following command to start Gateway:

    ```
    java -jar arms-gateway-1.7.0.jar
    ```

    **Note:** The version of Java Development Kit \(JDK\) must be later than JDK 1.7.

    By default, Gateway connects to the ARMS service in the China \(Hangzhou\) region. To connect Gateway to the ARMS service in another region, you can specify the region by using the -D parameter in the following way:

    ```
    java -jar -Darms.server.endpoint=arms-dc-bj.aliyuncs.com arms-gateway-1.7.0.jar
    ```

    -   China \(Hangzhou\): arms-dc-hz.aliyuncs.com
    -   China \(Beijing\): arms-dc-bj.aliyuncs.com
    -   China \(Shanghai\): arms-dc-sh.aliyuncs.com
    -   China \(Qingdao\): arms-dc-qd.aliyuncs.com
    -   China \(Shenzhen\): arms-dc-sz.aliyuncs.com
3.  Download the agent.

    You can log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home) and download the agent on the Add Application page. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Monitor Java applications/Manually install the ARMS agent for a Java application.md).

4.  Decompress the agent installation package.
5.  In the arms-agent.config file, change the value of the profiler.collector.ip parameter to the IP address of the proxy server.

    ```
    profiler.collector.ip={IP address of the proxy server}
    ```

6.  Start the application. In the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home), choose **Application Monitoring** \> **Applications** in the left-side navigation pane. Check whether monitoring data is reported. If monitoring data is reported, the application is connected to ARMS.

