# FAQ about installing the ARMS agent for Java applications

This topic lists FAQ about installing the Application Real-Time Monitoring Service \(ARMS\) agent for Java applications, and provides solutions.

## Is the ARMS agent compatible with agents of other Application Performance Management \(APM\) products, such as Pinpoint?

The ARMS agent is incompatible with agents of other APM products. Most APM technologies use the Automatic Storage Management \(ASM\) framework for bytecode instrumentation. If you install two agents, your code instrumentation will be implemented twice. Code instrumentation varies with manufacturers and code conflicts may cause serious performance issues. We do not recommend that you install multiple APM agents at the same time.

## What can I do if OutOfMemoryError is reported upon startup of an application after the ARMS agent is installed?

In this case, add the corresponding JVM heap memory parameter as appropriate.

If the initial value of heap memory size \(Xms\) is 512 MB and the maximum value of heap memory size \(Xmx\) is 2 GB, the configuration items are as follows: Adjust the values according to the actual requirement. In other environments such as Tomcat, add this parameter to JAVA\_OPTS of the configuration file.

```
   -Xms512M
   -Xmx2048M
```

If the `OutOfMemoryError: PermGen space` error is reported, add the following parameters:

```
   -XX:PermSize=256M 
   -XX:MaxPermSize=512M
```

## How do I check the network connectivity?

When deploying the ARMS agent, you can run the Telnet command to check if the target host is connected to the ARMS server network.

|Region|Endpoint|
|------|--------|
|China \(Hangzhou\)|arms-dc-hz.aliyuncs.com|
|China \(Beijing\)|arms-dc-bj.aliyuncs.com|
|China \(Shanghai\)|arms-dc-sh.aliyuncs.com|
|China \(Qingdao\)|arms-dc-qd.aliyuncs.com|
|China \(Shenzhen\)|arms-dc-sz.aliyuncs.com|

If you created an application in the China \(Shenzhen\) region of ARMS, you need to test if the environment in China \(Shenzhen\) is connected to the ARMS server network. The following result indicates that the network is connected:

```
telnet arms-dc-sz.aliyuncs.com 8443Trying 119.23.169.12...Connected to arms-dc-sz.aliyuncs.com.Escape character is '^]'.
```

**Note:** You must replace the endpoint according to your region. The port number remains unchanged.

## How do I check if the ARMS agent is successfully loaded?

1.  Run the following ps command to check if the ARMS agent is successfully loaded according to the command line start parameter:

    ```
    ps -ef | grep 'arms-bootstrap'
    ```

    When the ARMS agent is successfully loaded, the result is as follows:

2.  The arms.licenseKey and arms.appId attributes in the command line must be consistent with those displayed on the ARMS application setting page.


## What if no data is available after the ARMS agent is loaded?

1.  If the log file of the ARMS agent contains "send Agent metrics. no metrics.", verify whether your application has continuous external access requests, including HTTP requests, HSF requests, and Dubbo requests and whether the development framework is supported by the ARMS agent. For more information about third-party components and frameworks supported by the ARMS agent, see[Overview](/intl.en-US/Application monitoring/Overview.md) .

2.  Check whether the selected time range for query is correct. Select the past 15 minutes as the query time range and check whether monitoring data is available.

3.  If you start the ARMS agent by running the `-jar` command, check the setting of the command, and make sure that the -javaagent parameter is before `-jar`.

    ```
    java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=xxx -Darms.appId=xxx -jar demoApp.jar
    ```

4.  If the log file in the ArmsAgent/log/ directory contains the error "LicenseKey is invalid", check whether the region of your application is the same as the region of the ARMS agent.

5.  After your application is started, if the log sub-directory is unavailable in the ARMS agent directory since arms-bootstrap-1.7.0-SNAPSHOT.jar fails to be loaded, check whether the permission over the ARMS agent installation directory is correct.

6.  If the following error is reported when your application is started, check whether the arms-bootstrap-1.7.0-SNAPSHOT.jar package and the corresponding permission are correct.

7.  If there is still no monitoring data, pack the log file of the ARMS agent for Java applications in the ArmsAgent/log directory, and contact Customer Services of ARMS at DingTalk service account `@ARMS` for assistance.

8.  Check the JDK version. If the JDK version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the agent. We recommend that you upgrade the JDK or contact Customer Services of ARMS at DingTalk service account `@ARMS`.


## What can I do if no IP address or an incorrect IP address is displayed after the ARMS agent is successfully loaded?

1.  Run the `ifconfig -a` command to check the network configuration of the current machine. If the machine uses multiple network interface controllers \(NICs\), the IP address acquired by the ARMS agent is possibly not as expected, which is related to the network configuration.
2.  Solve the problem by using either of the following methods:
    -   Configure the `-DEAGLEEYE.LOCAL.IP=10.XX.XX.XX` JVM parameter explicitly.

        **Note:** Replace `10.XX.XX.XX` with the actual IP address.

    -   Configure the ARMS agent to obtain the `-DNETWORK.INTERFACE=eth0` JVM parameter, where `eth0` indicates the NIC name.

## Troubleshoot common errors contained in the log file \(ArmsAgent/log\) of the ARMS agent

-   If "LicenseKey is invalid" is reported:

    1.  First, make sure that your application is successfully created in ARMS and that AppId and LicenseKey were correctly set when the ARMS agent was installed.

    2.  ARMS is a multi-region environment. Therefore, you also need to check whether the download link of the ARMS agent is in the same region as your application.


