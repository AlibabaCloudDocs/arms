# Application environment

This topic describes how to view the environment information of an application, such as the IP address of the instance, execution duration, process ID, and Java Virtual Machine \(JVM\) version.

The application is monitored by Application Real-Time Monitoring Service \(ARMS\). For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the left-side navigation pane, click **Application Environment**.

    On the **Application Environment** page, view the environment information of the application.

    ![Application environment](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5073397161/p254728.png)

    |Parameter|Description|
    |---------|-----------|
    |Instance IP|The IP address of the instance where the application is deployed.|
    |Running Duration|The time elapsed for running the application.|
    |Process ID|The unique identifier of the application process.|
    |JVM Version|The version of the JVM that is used by the application.|
    |ARMS version probe|The version of the ARMS agent that is installed for the application.|
    |JVM Args|The parameter configuration for the JVM of the application.|
    |JVM parameter detection|The recommended parameter configuration for the JVM, which is calculated based on the physical memory of the instance where the application is deployed.|
    |Boot time|The time when the application was started.|
    |Hostname|The name of the instance where the application is deployed.|


