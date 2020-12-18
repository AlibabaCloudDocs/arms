# Manually install the ARMS agent for Java applications

After installing the Application Real-Time Monitoring Service \(ARMS\) agent, you can use it to monitor Java applications. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis. You can install the ARMS agent either manually or with one click. This topic describes how to manually install the ARMS agent for Java applications.

-   Ports 8442, 8443, and 8883 in the security group of your server have enabled outbound access on the public network over TCP. This operation is not required within a Virtual Private Cloud \(VPC\). For more information on how to enable the outbound access for Alibaba Cloud Elastic Compute Service \(ECS\) instances, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    **Note:** In addition to applications on Alibaba Cloud ECS instances, applications on public network servers can also access ARMS.

-   Make sure the third-party components or frameworks that your application uses are supported by ARMS. For more information about the compatibility list, see [Supported components and frameworks](/intl.en-US/Application monitoring/Reference/Supported components and frameworks.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, click **Create Application** in the upper-right corner.

3.  On the Create Application page, select **Java**, **Default Environment**, and **Manual Access**.

4.  Use either of the following methods to download the ARMS agent, and click **Next** on the Download Probe tab of the console.

    -   Method 1: Manually download the ARMS agent. On the Download Probe tab, click **Download Probe** to download the latest .zip file.
    -   Method 2: Run the `wget` command. Download the installation package based on your region by running the `wget` command.

        ```
        # China (Hangzhou)
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Shanghai)
        wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Qingdao)
        wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Beijing)
        wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Zhangjiakou)
        wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # China (Shenzhen)
        wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
        # Singapore
        wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
        # Finance Cloud
        wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
        ```

5.  Switch to the directory of the installation package. Run the following command to decompress the ARMS agent package to any working directory.

    ```
    unzip arms-php-agent.zip /{user.workspace}/ 
    ```

    **Note:** \{user.workspace\} is an example of the directory.

6.  On the Install Probe tab, view and save the LicenseKey.

7.  Use either of the following methods to add AppName and LicenseKey.

    -   Method 1: Change the JVM parameters according to the running environment of your application.

        **Note:** Replace `<LicenseKey>` with your LicenseKey, and replace `<AppName>` with your application name. Chinese characters currently cannot be used in application names. Replace \{user.workspace\} with the actual directory where the agent file is decompressed.

        -   Tomcat running environment

            -   On Linux or Mac, append the following configurations to the setenv.sh file under the \{TOMCAT\_HOME\}/bin directory.

                **Note:**

                If your Tomcat version does not contain the configuration file setenv.sh, open \{TOMCAT\_HOME\}/bin/catalina.sh, find `JAVA_OPTS` and append the following configuration to its value.

                Click to download a sample: [catalina.sh](https://arms-public.oss-cn-shanghai.aliyuncs.com/arms-agent/catalina.sh) \(definition on line 256\).

                ```
                JAVA_OPTS="$JAVA_OPTS -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName>" 
                ```

            -   On Windows, append the following configurations to the file \{TOMCAT\_HOME\}/bin/catalina.bat:

                ```
                set "JAVA_OPTS=%JAVA_OPTS% -javaagent:{user.workspace}ArmsAgentarms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName>" 
                ```

        -   Jetty running environment

            Append the following configuration to the configuration file \{JETTY\_HOME\}/start.ini:

            ```
            --exec # Open the note and just remove the number sign at the front -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> 
            ```

        -   Spring Boot running environment

            When starting the Spring Boot process, append the -javaagent parameter to the startup command.

            ```
            java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> -jar demoApp.jar 
            ```

            **Note:** Note that demoApp.jar is the JAR package name of the original application. Replace it with the correct JAR package name.

        -   Resin running environment

            1.  When starting the Resin process, append the following label to the configuration file conf/resion.xml:

                ```
                <server-default> <jvm-arg>-javaagent:{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar</jvm-arg> <jvm-arg>-Darms.licenseKey=<LicenseKey> </jvm-arg> <jvm-arg>-Darms.appName=<AppName> </jvm-xxxarg> </server-default> 
                ```

            2.  Append the following label to the conf/app-default.xml file:

                ```
                <library-loader path="{user.workspace}/ArmsAgent/plugin"/> 
                ```

        -   Windows running environment

            When starting the Java process on Windows, use backslashes \(\\\) as the separator in the agent loading path.

            ```
            {CMD}> java -javaagent:{user.workspace}ArmsAgentarms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> -jar {user.workspace}demoApp.jar 
            ```

            **Note:** Note that demoApp.jar is the JAR package name of the original application. Replace it with the correct JAR package name.

        To deploy the same application on multiple instances of one machine, use the parameter -Darms.agentId \(logic number, such as 001 and 002\) to distinguish between the connected JVM processes. Here is an example:

        ```
            java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> 
            -Darms.agentId=001 -jar demoApp.jar
        ```

    -   Method 2:
        1.  Modify the file arms-agent.config. Replace <LicenseKey\> with your LicenseKey and replace <AppName\> with the name of your application. Chinese characters currently cannot be used in application names.

            ```
            arms.licenseKey=<LicenseKey> arms.appName=<AppName>
            ```

        2.  Modify the JVM parameter by appending the following parameters to the starting script of the Java application.

            ```
            -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar 
            ```

            **Note:** Replace \{user.workspace\} with the correct directory where the ARMS agent is decompressed.

8.  Restart the Java application.


## Verification

After about one minute, if your Java application is displayed in the application list and has data reported, it is connected to ARMS.

## Uninstall the ARMS agent

1.  If you no longer need ARMS to monitor your Java application, you can delete the AppName and LicenseKey parameters added in [Step 8](https://www.alibabacloud.com/help/doc-detail/63797.htm#step-dv3-vvr-lxd) in the "Install the ARMS agent for Java applications."

2.  Restart the Java application.


## Change the name of an application in one click

If you want to change the name of an application, such as if you forget to change the name of the sample application Java-Demo to a custom name, you can change the application name without restarting the application or reinstalling the agent. For more information, see [t1884948.md\#li-6zu-n1q-egd](/intl.en-US/Application monitoring/Application monitoring FAQ.md).

[FAQ about updating the ARMS agent for Java applications](/intl.en-US/Application monitoring/FAQ about updating the ARMS agent for Java applications.md)

