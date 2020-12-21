# Create an application monitoring job

Application Real-Time Monitoring Service \(ARMS\) provides application monitoring features such as application trace analysis, local stack diagnosis, and business log troubleshooting. To monitor an application by using ARMS, you must create an application monitoring job.

## Background information

ARMS can monitor Java and PHP applications that run in various environments. This topic describes how to create an application monitoring job for a Java application that runs on an Elastic Compute Service \(ECS\) instance in the Tomcat environment. To ensure that you can monitor applications in different environments, ARMS allows you to install the ARMS agent manually or using scripts. However, to help you understand the general steps for creating an application monitoring job, this topic describes how to manually install the ARMS agent.

## Prerequisites

-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate and upgrade ARMS.md)

## Step 1: Obtain the license key

Perform the following steps to obtain the license key:

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
3.  On the Applications page, select a region in the top navigation bar, and click **Add Application** in the upper-right corner.
4.  Copy the license key at the top of the Add Application page.

    ![Download Agent](../images/p44353.png)


## Step 2: Configure the Tomcat runtime environment

Perform the following steps to configure the Tomcat runtime environment and set the required parameters in the configuration file:

1.  Open the \{TOMCAT\_HOME\}/bin/catalina.sh configuration file.

    **Note:** If your Tomcat does not contain the catalina.sh configuration file, find and open the \{TOMCAT\_HOME\}/bin/setenv.sh configuration file.

2.  Append the following configurations to the configuration file:

    **Note:** Replace <licenseKey\> in the following sample code with the license key that you obtained in Step 1. Replace <appName\> with the name of your application.

    ```
    JAVA_OPTS="$JAVA_OPTS -javaagent:/workspace/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<licenseKey> -Darms.appName=<appName>"
                        
    ```


The following sample code shows how to configure the Tomcat runtime environment:

## Step 3: Install the ARMS agent for Java applications

Perform the following steps to install the ARMS agent for Java applications and collect the monitoring data that you need:

1.  Run the wget command to download the compressed package of the ARMS agent for Java applications.

    **Note:** The China \(Hangzhou\) region is used in this example. For the download links of the ARMS agent for Java applications in other regions, see [Procedure](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md).

    ```
    # China (Hangzhou)
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

2.  Decompress the package of the ARMS agent for Java applications to a working directory. In this example, the working directory is workspace.

    ```
    unzip ArmsAgent.zip -d /workspace/
    ```


The following sample code shows how to install the ARMS agent for Java applications:

## Step 4: Restart Tomcat

1.  Go to the \{TOMCAT\_HOME\}/bin directory.
2.  Restart Tomcat.

    ```
    ./startup.sh
    ```


The following sample code shows how to restart Tomcat:

## Verify the result

After 2 to 3 minutes, log on to the [ARMS console](https://arms-intl.console.aliyun.com/). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. If your application \(specified by the <appName\> parameter\) appears on the Applications page, it indicates that the application monitoring job is created.

**Related topics**  


[Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md)

[Enable ARMS to monitor an EDAS application](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in EDAS in one click.md)

[Install the ARMS agent for a Java application deployed in Container Service for Kubernetes](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for Java applications in Container Service for Kubernetes.md)

[Install the ARMS agent for an application deployed in an open source Kubernetes environment](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in open-source Kubernetes environments.md)

[Install the ARMS agent for a Java application deployed in a Docker cluster](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for applications in Docker.md)

[Install the ARMS agent for a Java application by using scripts](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for Java applications by using scripts in one click.md)

[FAQ](/intl.en-US/Application monitoring/Application monitoring FAQ.md)

[Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Start monitoring PHP applications/Install the ARMS agent for common PHP applications.md)

[Install the ARMS agent for PHP applications deployed on multiple servers in standalone mode](/intl.en-US/Application monitoring/Start monitoring PHP applications/Install the arms agent for multi-site and standalone PHP applications.md)

[Install the ARMS agent for PHP applications in Container Service for Kubernetes]()

