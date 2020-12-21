# Create an application monitoring job

Application monitoring of Application Real-Time Monitoring Service \(ARMS\) can automatically discover application topologies, discover and monitor application interfaces, and capture abnormal and slow transactions. To start monitoring applications, you need to first create an application monitoring job.

## Background

Application monitoring of ARMS can monitor Java and PHP applications that run in multiple environments. This topic describes how to create an application monitoring job for a Java application that runs on an Elastic Compute Service \(ECS\) instance in Tomcat environment. In different application running environments, ARMS allows you to manually install the ARMS agent, install the ARMS agent with one click by using scripts, or automatically install the ARMS agent. However, to help you understand the general steps for creating an application monitoring job, this topic describes the procedure for manually installing the ARMS agent.

## Prerequisites

-   [Activate and upgrade ARMS](/intl.en-US/Quick start/Activate ARMS.md)
-   Ports 8442, 8443, and 8883 in the security group of your server have enabled outbound access on the public network over TCP. This operation is not required within a Virtual Private Cloud \(VPC\). For more information about how to set security group rules, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).


## Step 1: Obtain licenseKey.

Perform the following steps to obtain licenseKey, which will be used subsequently:

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Monitoring Jobs**.
2.  On top of the Monitoring Jobs page, select the target region, and click **Create Application** in the upper-right corner.
3.  On the Create Application page, select the following items:
    -   **Java**
    -   **Default**
    -   **Install Manually**
4.  On the **Download Probe** tab, click **Next**.
5.  On the Install Probe tab, copy the value of LicenseKey.

## Step 2: Configure the Tomcat running environment

Perform the following steps to configure the Tomcat running environment and set required parameters in the configuration file:

1.  Open the \{TOMCAT\_HOME\}/bin/catalina.sh configuration file.

    **Note:** If your Tomcat version does not have the catalina.sh configuration file, find and open the \{TOMCAT\_HOME\}/bin/setenv.sh configuration file.

2.  Add the following configuration to the configuration file:

    **Note:** In the following sample code, replace <licenseKey\> with your LicenseKey, and <appName\> with your application name.

    ```
    JAVA_OPTS="$JAVA_OPTS -javaagent:/workspace/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<licenseKey> -Darms.appName=<appName>"
                        
    ```


**Sample code: Configure the Tomcat running environment**

## Step 3: Install the ARMS agent for Java applications

Perform the following steps to install the ARMS agent for a Java application and collect the monitored data that you need:

1.  Run the wget command to download the compressed package of the ARMS agent for Java applications.

    **Note:** The China \(Hangzhou\) region is used in this example. For the compressed package download links of the ARMS agent for Java applications in other regions, see [Install the ARMS agent for Java applications](https://www.alibabacloud.com/help/doc-detail/63797.htm).

    ```
    # China (Hangzhou)
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

2.  Decompress the package of the ARMS agent for Java applications to the working directory. In this example, the working directory is workspace.

    ```
    unzip ArmsAgent.zip -d /workspace/
                        
    ```


**Sample code: Install the ARMS agent for Java applications**

## Step 4: Restart Tomcat

1.  Go to the \{TOMCAT\_HOME\}/bin directory.
2.  Restart Tomcat.

    ```
    ./startup.sh
    ```


**Sample code: Restart Tomcat**

## Verification

After two or three minutes, log on to the ARMS console. In the left-side navigation pane, choose **Application Monitoring** \> **Monitoring Jobs**. If your application named <appName\> appears on the Monitoring Jobs page, the application monitoring job is successfully created.

## More information

-   [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md)
-   [Install the ARMS agent for a Java application by using scripts](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for Java applications by using scripts in one click.md)
-   [FAQ about updating the ARMS agent for Java applications](/intl.en-US/Application monitoring/FAQ about updating the ARMS agent for Java applications.md)

