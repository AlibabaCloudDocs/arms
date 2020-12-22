# Manually install the ARMS agent for a Java application

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application, ARMS starts to monitor the Java application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. You can install the ARMS agent manually or using scripts. This topic describes how to manually install the ARMS agent for a Java application.

-   Ports 8442, 8443, and 8883 in the security group have been opened for TCP outbound access. For more information about how to grant outbound permissions to ECS, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    **Note:** In addition to applications on Alibaba Cloud ECS instances, applications on public network servers can also access ARMS.

-   Make sure your third-party components or frameworks are within the application monitoring compatibility list. For more information about the compatibility list, see [application monitoring compatibility list](/intl.en-US/Application monitoring/References/Java components and frameworks supported by ARMS.md).
-   If the JDK Version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the arms Agent. In this case, upgrade the JDK to the latest version in 1.8.X.


## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

3.  On the Applications page, click **Add Application** in the upper-right corner.

4.  On the Add Application page, perform the following operations:

    1.  Select **Java** as the **programming language of your application**.

    2.  Select **Default** as the **environment where your application is deployed**.

    3.  Select **Install Manually** as the **method to install the ARMS agent**.

5.  Use one of the following methods to download the ARMS agent, and then click Next on the Download Agent tab of the Add Application page.

    -   Method 1: Manually download the ARMS agent. On the **Download Agent** tab, click Download Agent.
    -   Method 2: Run the wget command. Download the installation package based on your region.

        **Note:** Use the public endpoint. If the download fails, use the VPC endpoint.

        |Region list|Public endpoint|VPC endpoint|
        |-----------|---------------|------------|
        |China \(Hangzhou\)|        ```

          wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Shanghai\)|        ```

          wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Qingdao\)|        ```

          wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Beijing\)|        ```

          wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Zhangjiakou\)|        ```

          wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Shenzhen\)|        ```

          wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China \(Hong Kong\)|        ```

          wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |Singapore|        ```

          wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |Japan \(Tokyo\)|        ```

          wget "http://arms-apm-japan.oss-ap-northeast-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-japan.oss-ap-northeast-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |US \(Silicon Valley\)|        ```

          wget "http://arms-apm-usw.oss-us-west-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-usw.oss-us-west-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China East 1 Finance|        ```

          wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China East 2 Finance|        ```

          wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |
        |China South 1 Finance|        ```

          wget "http://arms-apm-sz-finance.oss-cn-shenzhen-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ```

|        ```

          wget "https://arms-apm-sz-finance.oss-cn-shenzhen-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip 
        
        ``` |

6.  Go to the directory of the installation package. Run the following command to decompress the installation package to a working directory.

    ```
    unzip ArmsAgent.zip -d /{user.workspace}/ 
    ```

    **Note:** \{user.workspace\} is a sample directory. Replace it with an actual directory.

7.  Copy the license key at the top of the **Add Application** page.

    ![Obtain the license key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8283548061/p132858.png)

8.  Use one of the following methods to add the AppName and LicenseKey parameters:

    **Note:** Replace `{LicenseKey}` in the sample code with your license key. Replace `{AppName}` with your application name. The application name cannot contain Chinese characters. Replace `{user.workspace}` with the directory where the ARMS agent is decompressed. Replace demoApp.jar with the actual JAR package address.

    -   Method 1: Edit the JVM parameters based on the runtime environment of your application.

        |Runtime environment|Procedure|
        |-------------------|---------|
        |Tomcat \(Linux or macOS\)|Append the following configurations to the \{TOMCAT\_HOME\}/bin/setenv.sh file:

        ```
JAVA_OPTS="$JAVA_OPTS -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}" 
        ```

If your Tomcat does not contain the setenv.sh configuration file, open the \{TOMCAT\_HOME\}/bin/catalina.sh file and append the preceding configurations to the JAVA\_OPTS parameter. For more information, see Row 256 in [catalina.sh](https://arms-public.oss-cn-shanghai.aliyuncs.com/arms-agent/catalina.sh). |
        |Tomcat \(Windows\)|Append the following configurations to the \{TOMCAT\_HOME\}/bin/catalina.bat file:        ```
set "JAVA_OPTS=%JAVA_OPTS% -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}" 
        ```

If the preceding setting does not take effect, append the following configurations to the \{TOMCAT\_HOME\}/bin/catalina.bat file:

        ```
set "CATALINA_OPTS=-javaagent:/{user.workspace}/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName}"
        ``` |
        |Jetty|Append the following configurations to the \{JETTY\_HOME\}/start.ini configuration file:

        ```
--exec
-javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
-Darms.licenseKey={LicenseKey}
-Darms.appName={AppName} 
        ``` |
        |Spring Boot|When you start the Spring Boot process, append the -javaagent parameter to the startup command:

        ```
java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -jar demoApp.jar 
        ``` |
        |Resin|When you start the Resin process, append the following tag to the conf/resion.xml configuration file:

        ```
<server-default>
    <jvm-arg>-javaagent:{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar</jvm-arg>
    <jvm-arg>-Darms.licenseKey={LicenseKey}</jvm-arg>
    <jvm-arg>-Darms.appName={AppName}</jvm-arg>
</server-default> 
        ```

Append the following tag to the conf/app-default.xml file:

        ```
<library-loader path="{user.workspace}/ArmsAgent/plugin"/> 
        ``` |
        |Windows|When you start the Java process, use a backslash \(\\\) as the delimiter in the mount path of the ARMS agent.

        ```
{CMD}} java -javaagent:\{user.workspace}\ArmsAgent\arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -jar {user.workspace}\demoApp.jar 
        ``` |

        To deploy multiple instances of the same application on a server, you can differentiate the JVM processes by setting the -Darms.agentId parameter to a logical number. Example:

        ```
        java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey={LicenseKey} -Darms.appName={AppName} -Darms.agentId=001 -jar demoApp.jar
        ```

    -   Method 2:
        1.  Append the following configurations to the arms-agent.config file:

            ```
            arms.licenseKey={LicenseKey} arms.appName={AppName}
            ```

        2.  Append the following parameters to the startup script of the Java application:

            ```
            -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar 
            ```

9.  Restart the Java application.


## Verify the result

After about 1 minute, if your application is displayed in the application list and some data records are sent, it indicates that your application is monitored by ARMS.

## Uninstall the ARMS agent

If you no longer need ARMS to monitor your Java application, perform the following steps to uninstall the ARMS agent.

1.  Delete all parameters that you added in [Step 8](#step_configure_licensekey), such as \{AppName\} and \{LicenseKey\}.

2.  Restart the Java application.


## Change the application name

If you forget to change the sample name Java-Demo to a custom name, you can change the application name by performing a few operations. You do not need to restart the application or reinstall the ARMS agent. For more information, see [How do I modify the name of a common Java application on which the ARMS agent is manually installed?](/intl.en-US/Application monitoring/FAQ.mdsection_sx9_df1_3pq)

**Related topics**  


[FAQ](/intl.en-US/Application monitoring/FAQ.md)

