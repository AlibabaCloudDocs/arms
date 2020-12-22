# Why is no monitoring data displayed in the ARMS console after I install an ARMS agent?

## Condition

After an ARMS agent is installed, no monitoring data is displayed in the ARMS console.

## Cause

This problem may occur because the application does not have continuous external access requests, the region of the application is different from that of the ARMS agent, or the permissions on the ARMS agent installation directory are invalid.

1.  If the log file of the ARMS agent contains "send agent metrics. no metrics.", verify whether the development framework is supported by the ARMS agent and whether your application has continuous external access requests, including HTTP requests, HSF requests, and Dubbo requests. For more information about third-party components and frameworks supported by the ARMS agent, see [Java components and frameworks supported by ARMS](/intl.en-US/Application monitoring/References/Java components and frameworks supported by ARMS.md) and [PHP components and frameworks supported by ARMS Application Monitoring](/intl.en-US/Application monitoring/References/PHP components and frameworks supported by ARMS Application Monitoring.md).

2.  Check whether the selected time range to query is correct. Select the last 15 minutes as the query time range and check whether monitoring data is displayed.

3.  If you start the ARMS agent by running the `-jar` command, check the configuration of the command line and make sure that the -javaagent parameter is before `-jar`.

    ```
    java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=xxx -Darms.appName=xxx -jar demoApp.jar
    ```

4.  If the log in ArmsAgent/log/ contains the LicenseKey is invalid. error, check whether the region of your application is the same as that of the ARMS agent.

5.  If the log subdirectory does not exist in the ArmsAgent directory after your application is started, this is because arms-bootstrap-1.7.0-SNAPSHOT.jar failed to be loaded. Check whether the permissions on the ARMS agent installation directory are valid.

6.  If the following error is reported when your application is started, check whether the arms-bootstrap-1.7.0-SNAPSHOT.jar package and the permissions are correct.

    ![Application Start Error](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5096358061/p43213.png)

7.  If no monitoring data is displayed, pack the log file of the ARMS agent for Java applications in the ArmsAgent/log directory, and contact customer services of ARMS at DingTalk service account `arms160804` for assistance.

8.  Check the JDK version.

    -   If the JDK version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the agent. We recommend that you upgrade the JDK or contact customer services of ARMS at DingTalk service account `arms160804`.
    -   If the JDK version is 1.10.X, download the correct agent installation package from one of the following addresses:
        -   [China \(Hangzhou\)](https://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Shanghai\)](https://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Qingdao\)](https://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Beijing\)](https://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Zhangjiakou\)](https://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Shenzhen\)](https://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [China \(Hong Kong\)](https://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)

