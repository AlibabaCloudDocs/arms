# Install the ARMS agent for a Java application by using scripts

You can use scripts to install the Application Real-Time Monitoring Service \(ARMS\) agent for a Java application. To monitor the application, you do not need to restart the application. We recommend that you choose this installation method if you are using ARMS for the first time. If you restart the Java application, ARMS automatically loads the ARMS agent and monitors the application.

-   Ports 8442, 8443, and 8883 in the security group have been opened for TCP outbound access. For more information about how to grant outbound permissions to ECS, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    **Note:** In addition to applications on Alibaba Cloud ECS instances, applications on public network servers can also access ARMS.

-   Make sure your third-party components or frameworks are within the application monitoring compatibility list. For more information about the compatibility list, see [application monitoring compatibility list](/intl.en-US/Application monitoring/References/Java components and frameworks supported by ARMS.md).
-   If you have manually installed the ARMS agent for the Java application, you must uninstall the ARMS agent before you can use scripts to install the ARMS agent. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md).
-   If the JDK Version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the arms Agent. In this case, upgrade the JDK to the latest version in 1.8.X.


## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  On the Applications page, select a region in the top navigation bar, and click **Add Application** in the upper-right corner.

4.  On the Add Application page, perform the following operations:

    1.  Select **Java** as the programming language of your application.

    2.  Select **Default** as the environment where your application is deployed.

    3.  Select **Install with Script** as the method to install the ARMS agent.

    ![Access Agent](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4445658061/p44367.png)

5.  Copy the license key at the top of the Add Application page.

6.  Run the installation script that corresponds to your region.

    |Region|Installation script|
    |------|-------------------|
    |China \(Hangzhou\)|    ```
wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China \(Shanghai\)|    ```
wget -O- http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China \(Qingdao\)|    ```
wget -O- http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China \(Beijing\)|    ```
wget -O- http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China \(Shenzhen\)|    ```
wget -O- http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China \(Hong Kong\)|    ```
wget -O- http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |Singapore \(Singapore\)|    ```
wget -O- http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |Japan \(Tokyo\)|    ```
wget -O- http://arms-apm-japan.oss-ap-northeast-1.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |US \(Silicon Valley\)|    ```
wget -O- http://arms-apm-usw.oss-us-west-1.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |
    |China East 1 Finance|    ```
wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ``` |

    **Note:**

    -   Replace `<licenseKey>` with your license key.
    -   Replace `Java-Demo` with the name of your application. The application name cannot contain Chinese characters.
    -   After you run the installation script, it automatically downloads the latest ARMS agent.
    -   If your server has only one Java process, the installation script installs the ARMS agent on this process by default. If your server has multiple Java processes, select a process to install the ARMS agent.

## Verify the result

After about 1 minute, if your application is displayed in the application list and some data records are sent, it indicates that your application is monitored by ARMS.

## Uninstall the ARMS Agent

1.  If you no longer want to use ARMS to monitor your Java applications, run the `jps -l` command to view all processes and find the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` in the returned results.

    In this example, the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` is 62857.

    ![Kill Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4872485951/p43111.png)

2.  Run the `kill -9 <process ID>` command.

    Example: `kill -9 62857`.

3.  Run the `rm -rf /.arms /root/.arms` command.

4.  Restart your application.


## Change the application name

If you forget to change the sample name Java-Demo to a custom name, you can change the application name by performing a few operations. You do not need to restart the application or reinstall the ARMS agent. For more information, see [How can I change the name of a Java application after I use scripts to install the ARMS agent?](/intl.en-US/Application monitoring/FAQ.mdsection_dv7_df9_oz2)

## FAQ

1.  How can I handle the following getcwd error when I run the installation script to install the ARMS agent?

    ```
    shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory Error occurred during initialization of VM java.lang.Error: Properties init: Could not determine current working directory. at java.lang.System.initProperties(Native Method) at java.lang.System.initializeSystemClass(System.java:1119)
    ```

    The possible cause is that the current directory is deleted by mistake when you run the installation script. To solve this issue, run the `cd` command and then run the installation script again.

2.  Where do I view logs after I run the installation script to install the ARMS agent?

    The default directory of logs is /root/.arms/supervisor/logs/arms-supervisor.log. If no logs are available in this directory, run the `ps -ef |grep arms` command to view the directory where logs are stored.


**Related topics**  


[FAQ](/intl.en-US/Application monitoring/FAQ.md)

