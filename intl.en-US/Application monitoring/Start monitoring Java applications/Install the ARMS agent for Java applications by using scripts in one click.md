# Install the ARMS agent for Java applications by using scripts in one click

Application Real-Time Monitoring Service \(ARMS\)'s one-click agent installation for Java applications does not require restarting the applications for the installed agent to take effect. The ARMS agent starts monitoring applications once installed, which is suitable for users who are using the ARMS agent for the first time. When a Java application restarts, the ARMS agent is automatically loaded, and the application is automatically connected to ARMS application monitoring.

-   Ports 8442, 8443, and 8883 in the security group of your server have enabled outbound access on the public network over TCP. This operation is not required within a Virtual Private Cloud \(VPC\). For more information on how to enable the outbound access for Alibaba Cloud Elastic Compute Service \(ECS\) instances, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    **Note:** In addition to applications on Alibaba Cloud ECS instances, applications on public network servers can also access ARMS.

-   Make sure the third-party components or frameworks that your application uses are supported by ARMS. For more information about the compatibility list, see [Supported components and frameworks](/intl.en-US/Application monitoring/Reference/Supported components and frameworks.md).
-   If your application is manually connected to ARMS application monitoring, you need to uninstall the ARMS agent before you can use the one-click method. For more information, see [Uninstall the ARMS agent](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for Java applications.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

2.  On the Applications page, click **Create Application** in the upper-right corner.

3.  On the Create Application page, select **Java**, **Default Environment**, and **One-Click Access**. Then view and save the LicenseKey.

    ![Access the agent](../images/p44367.png)

4.  Run the installation script corresponding to your region.

    ```
    # China (Hangzhou)
    wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # China (Shanghai)
    wget -O- http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # China (Qingdao)
    wget -O- http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # China (Beijing)
    wget -O- http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # China (Shenzhen)
    wget -O- http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # Singapore
    wget -O- http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    # Finance Cloud
    wget -O- http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/install.sh | sh && ~/.arms/supervisor/cli.sh <licenseKey> Java-Demo
    ```

    **Note:**

    -   Replace `<licenseKey>` with your LicenseKey.
    -   Replace `Java-Demo` with the name of your application. Chinese characters currently cannot be used in application names.
    -   After the installation script is run, it automatically downloads the latest ARMS agent.
    -   If your server has only one Java process, the installation script installs the ARMS agent for this process by default. If your server has multiple Java processes, select a process to install the ARMS agent.

## Verification

After about one minute, if your application is displayed in the application list and has data reported, it is connected to ARMS.

## Uninstall the ARMS agent

1.  If you no longer need ARMS to monitor your Java application, you can run the `jps -l` command to view all processes and find the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` in the command output.

    In this example, the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` is 62857.

    ![Kill process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4872485951/p43111.png)

2.  Run the `kill -9 <process ID>` command, for example, `kill -9 62857`.

3.  Run the `rm -rf /.arms /root/.arms` command.

4.  Restart your application.


## Change the name of an application in one click

If you want to change the name of an application, such as if you forget to change the name of the sample application Java-Demo to a custom name, you can change the application name without restarting the application or reinstalling the agent.

## FAQ

1.  How do I handle the following getcwd errors when running the one-click ARMS agent installation script?

    ```
    shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory Error occurred during initialization of VM java.lang.Error: Properties init: Could not determine current working directory. at java.lang.System.initProperties(Native Method) at java.lang.System.initializeSystemClass(System.java:1119)
    ```

    The possible cause is that the current directory was deleted by mistake when the script ran. To solve this problem, run `cd` and then run the script again.

2.  Where do I view the log when installing the ARMS agent with one click?

    The default directory of the log is /root/.arms/supervisor/logs/arms-supervisor.log. If no logs are available in this directory, run `ps -ef |grep arms` to view the directory where the logs are stored.


