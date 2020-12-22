---
keyword: [Agent upgrade, Application name update]
---

# FAQ

This topic provides answers to commonly asked questions about the application monitoring feature of Application Real-time Management Service \(ARMS\).

## Overview

-   FAQ about manually installing the ARMS agent for Java applications
    -   [Is the ARMS agent compatible with the agents of other Application Performance Management \(APM\) products, such as Pinpoint?](#section_gfn_ya7_099)
    -   [What do I do if OutOfMemoryError is reported when I start an application after the ARMS agent is installed?](#section_ci4_3iq_iza)
    -   [How do I test network connectivity?](#section_9ym_wo6_9cm)
    -   [How do I check whether the ARMS agent is successfully installed?](#section_176_ebo_zaf)
    -   [Why is no monitoring data displayed in the ARMS console after I install an ARMS agent?](#section_659_3mt_w0m)
    -   [What do I do if no IP address or an incorrect IP address is displayed after the ARMS agent is installed?](#section_xg0_zwo_6aa)
    -   [How do I troubleshoot common errors contained in the log files of the ARMS agent stored in the ArmsAgent/log folder?](#section_2ad_7xt_58o)
    -   [How do I deploy multiple instances on a single machine?](#section_4gb_a5i_6r9)
-   FAQ about installing the ARMS agent for Java applications with one click
    -   [What do I do when getcwd errors are reported when I run the script to access a Java application?](#section_cya_bmz_j1n)
    -   [Where do I view the logs after I install the ARMS agent with one click?](#section_di2_2lw_3ip)
-   FAQ about installing the ARMS agent for Java applications deployed on ECS instances with one click
    -   [What do I do if the ARMS agent cannot be installed?](#section_buk_rya_wlc)
    -   [What do I do if the information about the processes of the ECS instance is inaccurate after the ARMS agent is installed?](#section_wqg_0fl_nfo)
    -   [What do I do if I cannot enable ARMS application monitoring for a process on an ECS instance?](#section_qjw_ejq_57y)
-   FAQ about installing the ARMS agent for Java applications in Container Service for Kubernetes \(ACK\) clusters
    -   [Why is there no data displayed in Application Monitoring after the ARMS agent is installed on a Java application in an ACK cluster?](#section_wya_dhr_4sg)
-   FAQ about installing the ARMS agent for Java applications in open-source Kubernetes environments
    -   [What do I do if the application cannot be started?](#section_29p_abj_wnf)
    -   [How do I view the logs of the ARMS agent?](#section_639_vj8_l7a)
-   FAQ about modifying the names of Java applications without reinstalling the ARMS agent
    -   [How do I modify the name of a common Java application on which the ARMS agent is manually installed?](#section_sx9_df1_3pq)
    -   [How do I modify the name of a Java application deployed in an ACK cluster?](#section_4h6_839_xdz)
    -   [How do I modify the name of a Java application deployed in Enterprise Distributed Application Service \(EDAS\)?](#section_clm_x1z_cap)
-   FAQ about uninstalling the ARMS agent
    -   [How do I uninstall the ARMS agent that is manually installed?](#section_2je_5ub_m2q)
    -   [How do I uninstall the ARMS agent that is installed with one click?](#section_lcu_dvl_fyl)
    -   [How do I uninstall the ARMS agent installed on a Java application deployed on an ECS instance?](#section_2f1_20j_xgy)
    -   [How do I uninstall the ARMS agent installed on a Java application in an ACK cluster?](#section_is9_8a3_de4)
    -   [How do I uninstall the ARMS agent installed on a Java application in an open-source Kubernetes environment?](#section_38x_tgd_1t8)
    -   [How do I uninstall the ARMS agent installed on a Java application in Docker?](#section_okg_1fg_oam)
    -   [How do I uninstall the ARMS agent installed on a PHP application?](#section_k86_g74_0j3)
    -   [How do I uninstall the ARMS agent installed on a PHP application in an ACK cluster?](#section_23e_pkg_iue)
-   Other FAQ
    -   [What do I do if the data of my application with the OpenFeign component is incomplete in ARMS?](#section_200_a7a_i2w)

## Is the ARMS agent compatible with the agents of other Application Performance Management \(APM\) products, such as Pinpoint?

The ARMS agent is incompatible with the agents of other APM products. APM is implemented using bytecode instrumentation based on the ASM framework. If you install two agents, bytecode instrumentation is performed twice on the code. Agents developed by different vendors use different code to implement bytecode instrumentation. Therefore, if you install multiple agents, performance issues may occur due to code conflicts. We recommend that you do not install the agents of other APM products.

[\[Back to the top\]](#sc_toc)

## What do I do if OutOfMemoryError is reported when I start an application after the ARMS agent is installed?

Add the corresponding heap memory parameters to the start command to increase the memory of the JVM. In the following example, the initial value of heap memory size \(Xms\) is 512 MB and the maximum value of heap memory size \(Xmx\) is 2 GB.

**Note:** Adjust the values based on your actual requirement. In other environments such as Tomcat, add this parameter to JAVA\_OPTS of the configuration file.

```
   -Xms512M
   -Xmx2048M
```

If the `OutOfMemoryError: PermGen space` error is reported, add the following parameters to the start command:

```
   -XX:PermSize=256M 
   -XX:MaxPermSize=512M
```

If the `OutOfMemoryError: metaspace` error is reported, add the following parameters to the start command:

```
   -XX:MetaspaceSize=256M 
   -XX:MaxMetaspaceSize=512M
```

[\[Back to the top\]](#sc_toc)

## How do I test network connectivity?

Before you install the ARMS agent, make sure that the 8883, 8443, and 8442 ports can be accessed. You can run the Telnet command to check whether the target host is connected to the ARMS server network. For example, to test the connectivity to the China \(Shenzhen\) region, log on to the host on which the application is deployed and run the following commands:

```
telnet arms-dc-sz.aliyuncs.com 8883
telnet arms-dc-sz.aliyuncs.com 8443
telnet arms-dc-sz.aliyuncs.com 8442
```

**Note:** Replace the domain names in the preceding commands with the actual endpoints of ARMS application monitoring. Note that the endpoint of ARMS application monitoring varies depending on if you access it from classic networks and the Internet or VPCs.

|Region|Endpoint for access from classic networks and the Internet|Endpoint for access from VPC|
|------|----------------------------------------------------------|----------------------------|
|China \(Hangzhou\)|arms-dc-hz.aliyuncs.com|arms-dc-hz-internal.aliyuncs.com|
|China \(Beijing\)|arms-dc-bj.aliyuncs.com|arms-dc-bj-internal.aliyuncs.com|
|China \(Shanghai\)|arms-dc-sh.aliyuncs.com|arms-dc-sh-internal.aliyuncs.com|
|China \(Qingdao\)|arms-dc-qd.aliyuncs.com|arms-dc-qd-internal.aliyuncs.com|
|China \(Shenzhen\)|arms-dc-sz.aliyuncs.com|arms-dc-sz-internal.aliyuncs.com|
|China \(Zhangjiakou\)|arms-dc-zb.aliyuncs.com|arms-dc-zb-internal.aliyuncs.com|
|China \(Hong Kong\)|arms-dc-hk.aliyuncs.com|arms-dc-hk-internal.aliyuncs.com|
|Singapore|arms-dc-sg.aliyuncs.com|arms-dc-sg-internal.aliyuncs.com|
|Regions for Alibaba GovCloud|arms-dc-gov.aliyuncs.com|arms-dc-gov-internal.aliyuncs.com|
|Finance Cloud of China \(Hangzhou\)|arms-dc-hz-finance.aliyuncs.com|arms-dc-hz-finance-internal.aliyuncs.com|

[\[Back to the top\]](#sc_toc)

## How do I check whether the ARMS agent is successfully installed?

Run the following ps command to check whether the ARMS agent is successfully installed based on parameters in the start command.

```
ps -ef | grep 'arms-bootstrap'
```

The results shown in the following figure indicates that the ARMS agent is successfully installed.

![ARMS Agent](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7569658061/p63971.png)

The value of Darms.licenseKey in the command must be the same as the license key value displayed on the **Add Application** page in the ARMS console.

![ARMS Access Application](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1948974951/p63972.png)

[\[Back to the top\]](#sc_toc)

## Why is no monitoring data displayed in the ARMS console after I install an ARMS agent?

1.  If the log of the ARMS agent contains `send agent metrics. no metrics.`, check whether your application is continuously accessed by external requests, including HTTP requests, HSF requests, and Dubbo requests and whether the development framework is supported by the ARMS agent. For more information about third-party components and frameworks supported by the ARMS agent, see [Overview](/intl.en-US/Application monitoring/Overview.md).
2.  Check whether the selected time range for query is correct. Select the past 15 minutes as the time range for query and check whether monitoring data is displayed.
3.  If you start the ARMS agent by running the `-jar` command, check the setting of the command and make sure that the -javaagent parameter is before `-jar`. The following command provides an example on how to add parameters to the start command:

    ```
    java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=xxx -Darms.appName=xxx -jar demoApp.jar
    ```

4.  If the logs stored in ArmsAgent/log/ contains the "LicenseKey is invalid." error, check whether the region of your application is the same as that of the ARMS agent.
5.  After your application is started, if the log folder does not exist in the ArmsAgent folder, it indicates that arms-bootstrap-1.7.0-SNAPSHOT.jar fails to be loaded. Check whether the permissions of the ArmsAgent folder are correct.
6.  If the following error is reported when your application is started, check whether the arms-bootstrap-1.7.0-SNAPSHOT.jar package and the corresponding permissions are correct.

    ```
    Error opening zip file or JAR manifest missing: /root/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
    Error occurred during initialization of VM
    agent library failed to init: instrument
    ```

7.  If no monitoring data is displayed, compress the logs of the ARMS agent for Java applications in the ArmsAgent/log folder into a compressed file, and contact the DingTalk account `arms160804` for support.
8.  Check the JDK version. If the JDK version is 1.8.0\_25 or 1.8.0\_31, you may fail to install the agent. We recommend that you upgrade the JDK or contact the DingTalk account `arms160804`.


[\[Back to the top\]](#sc_toc)

## What do I do if no IP address or an incorrect IP address is displayed after the ARMS agent is installed?

1.  Run the ifconfig -a command to check the network configuration of the current machine. If the machine uses multiple network interface controllers \(NICs\), the IP address obtained by the ARMS agent may be inconsistent with the actual IP address due to network configurations.
2.  You can solve the problem by using one of the following methods:
    -   Configure the `-DEAGLEEYE.LOCAL.IP=10.XX.XX.XX` parameter of the JVM.

        **Note:** Replace `10.XX.XX.XX` with the actual IP address.

    -   Configure the ARMS agent to obtain the value of the `-DNETWORK.INTERFACE=eth0` parameter, in which `eth0` indicates the NIC name.

[\[Back to the top\]](#sc_toc)

## How do I troubleshoot common errors contained in the log files of the ARMS agent stored in the ArmsAgent/log folder?

If the "LicenseKey is invalid" error is contained in the logs, perform the following operations to troubleshoot the error:

1.  Make sure that the application is created in ARMS and the LicenseKey that you specified when the ARMS agent is installed is correct.
2.  ARMS supports multiple regions. Therefore, check whether the download URL of the ARMS agent is in the same region as your application.

[\[Back to the top\]](#sc_toc)

## How do I deploy multiple instances on a single machine?

To deploy multiple instances of an application on a single machine, configure the -Darms.agentId parameter to specify the JVM process to connect. This parameter indicates a logical number. Examples: 001 and 002. The following command provides an example on how to deploy multiple instances on a single machine:

```
java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=<LicenseKey> -Darms.appName=<AppName> -Darms.agentId=001 -jar demoApp.jar
```

[\[Back to the top\]](#sc_toc)

## What do I do when getcwd errors are reported when I run the script to access a Java application?

The following error message is returned after you run the script to access the Java application with one click:

```
shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory Error occurred during initialization of VM java.lang.Error: Properties init: Could not determine current working directory. at java.lang.System.initProperties(Native Method) at java.lang.System.initializeSystemClass(System.java:1119)
```

This may because that the current directory is accidentally deleted when the script is running. To solve this problem, run the `cd` command and then run the script again.

[\[Back to the top\]](#sc_toc)

## Where do I view the logs after I install the ARMS agent with one click?

By default, the logs are stored in /root/.arms/supervisor/logs/. If no logs are stored in this folder, run `ps -ef |grep arms` to view the folder where the logs are stored.

[\[Back to the top\]](#sc_toc)

## What do I do if the ARMS agent cannot be installed?

1.  Make sure that your ECS instance can access the download URL of the ARMS agent over the Internet in the region in which the ECS instance is located.

    |Region|Download URL in Internet|
    |------|------------------------|
    |China \(Hangzhou\)|    ```
http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh
    ``` |
    |China \(Shanghai\)|    ```
http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh
    ``` |
    |China \(Qingdao\)|    ```
http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh
    ``` |
    |China \(Beijing\)|    ```
http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh
    ``` |
    |China \(Shenzhen\)|    ```
http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh
    ``` |
    |Singapore|    ```
http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh
    ``` |

2.  Make sure that your ECS instance can access the ARMS console.
    -   [ARMS console for regions in China](https://arms.console.aliyun.com/)
    -   [ARMS console for the Singapore region](https://arms-ap-southeast-1.console.aliyun.com)
3.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) and perform the following operations:
    1.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.
    2.  On the **Cloud Assistant** page, click the Commands tab, select **Command Name** in the search box, enter `InstallJavaAgent`, and press the Enter key.

        **Note:** If no result is returned for the search, contact the DingTalk account `arms160804`.

    3.  On the **Cloud Assistant** page, click the **Command Execution Result** tab and enter the ID of the `InstallJavaAgent`. In the search results, click **View** in the **Actions** column corresponding to the command and check whether the `command` is successfully executed. If the command is not successfully executed, troubleshoot the errors based on the execution results. For example, if the problems occur because the disk of the ECS instance is full or the ARMS agent is not installed, you can clear the disk or install the ARMS agent. If the errors cannot be resolved, send the execution results to the DingTalk account `arms160804` for support.

[\[Back to the top\]](#sc_toc)

## What do I do if the information about the processes of the ECS instance is inaccurate after the ARMS agent is installed?

If the information about the processes of the ECS instance is not displayed or is inaccurate after the ARMS agent is installed, click the **-** icon on the left side of the ECS instance and click the **+** icon to refresh the data. If the problem retains, contact the DingTalk account `arms160804` for support.

[\[Back to the top\]](#sc_toc)

## What do I do if I cannot enable ARMS application monitoring for a process on an ECS instance?

On the ECS instance, check whether the `/root/.arms/supervisor/logs/arms-supervisor.log` file contains errors. If the log file contains errors, troubleshoot the error based on the error message. If the error cannot be solved, contact the DingTalk account `arms160804` for support.

[\[Back to the top\]](#sc_toc)

## Why is there no data displayed in Application Monitoring after the ARMS agent is installed on a Java application in an ACK cluster?

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, choose **Clusters**. On the Clusters page, click **Applications** in the Actions column corresponding to the cluster in which the Java application is deployed.

3.  At the top of the Pods tab, select the namespace in which your application resides. Click **Edit** next to the application.

4.  In the Edit YAML dialog box, check whether the YAML file contains initContainers.

    -   If initContainers is not contained in the YAML file, the pod has not been injected to arms-init-container. Perform [Step 5](#step_3y6_ddh_qfm).
    -   If initContainers is contained in the YAML file, the pod has been injected to arms-init-container. Perform [Step 8](#step_2xg_hy4_0h8).
5.  At the top of the Pods tab, set Namespace to **arms-pilot**. Check whether any pods whose names contain the **arms-pilot** prefix exist in the Pod list.

    -   If pods whose names contain the prefix exist, perform [Step 6](#step_w3r_w45_eav).
    -   If pods whose names contain the prefix do not exist, install arms-pilot from the application market. For more information, see [Install the ARMS agent for Java applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
6.  On the Deployments or StatefulSets tab, choose **More** \> **View in YAML** in the Actions column. In the Edit YAML dialog box, check whether the YAML file contains the following annotations.

    ```
    annotations:
      armsPilotAutoEnable: 'on'
      armsPilotCreateAppName: <your-deployment-name>
    ```

    -   If the YAML file contains the annotations, perform [Step 7](#step_nah_s9j_wrd).
    -   If the YAML file does not contain the annotations, add the preceding annotations to the spec \> template \> metadata section in the Edit YAML dialog box, replace `<your-deployment-name>` with your application name. Then, click **Update**.
7.  On the Pods tab, click **Logs** next to the required pod to check whether the pod logs of arms-pilot reports an STS error in the `"Message":"STS error"` format.

    -   If the error is reported, authorize the cluster of the application and restart the pod of the application. For more information, see [Install the ARMS agent for Java applications in Container Service for Kubernetes](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application deployed in Container Service for Kubernetes.md).
    -   If the error is not reported, contact the DingTalk account arms160804 for support.
8.  On the Pods tab, click **Edit** next to the required pod. In the Edit YAML dialog box, check whether the YAML file contains the following javaagent parameter:

    ```
    -javaagent:/home/admin/.opt/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar
    ```

    -   If the YAML file contains the parameter, find the pod of the application on the Pods page, and click **Terminal** next to the target pod to access the command line page. Run the following command to check whether any log file name is suffixed with .log. Then, contact the DingTalk account arms160804.

        ```
        cd /home/admin/.opt/ArmsAgent/logs
        ```

    -   If the YAML file does not contain the parameter, contact the DingTalk account arms160804 for support.

[\[Back to the top\]](#sc_toc)

## What do I do if the application cannot be started?

Run the following command to view the arms-pilot-system logs and troubleshoot the problem based on the logs:

```
kubectl logs -f {arms-pilot-arms-pilot-XXX} -n arms-pilot-system
```

[\[Back to the top\]](#sc_toc)

## How do I view the logs of the ARMS agent?

On the worker of the ACK cluster, view the /home/admin/.opt/ArmsAgent/logs/xxxx.log files.

[\[Back to the top\]](#sc_toc)

## How do I modify the name of a common Java application on which the ARMS agent is manually installed?

Common Java applications indicate Java applications other than those deployed on ECS instances. If you manually install the ARMS agent on the application, the directory of the agent is specified by you during the installation.

You can check the version of the ARMS agent by viewing the Version file in the directory of the agent. For example, `2.5.8_cf020486_20190816150025` indicates that the version of the ARMS agent is 2.5.8 and was released on August 16, 2019.

-   If the version of the ARMS agent is earlier than 2.5.8.1, uninstall the agent and install it again. You can specify a new application name when you reinstall the agent.
    -   For more information about how to uninstall the ARMS agent that is manually installed, see[How do I uninstall the ARMS agent that is manually installed?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-2je-5ub-m2q)
    -   For more information about how to uninstall the ARMS agent that is installed with one click, see[How do I uninstall the ARMS agent that is installed with one click?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-lcu-dvl-fyl)
    -   For more information about how to uninstall the ARMS agent installed on applications in ECS instances, see[How do I uninstall the ARMS agent installed on applications in ECS instances?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-2f1-20j-xgy)
-   If the version of the ARMS agent is 2.5.8.1 or later, you can perform the following steps to modify the name of the Java application without reinstalling the ARMS agent.

    **Note:** ARMS agents downloaded after August 20, 2019 support this feature.


1.  Run one of the following commands to download and decompress Supervisor from the Internet or VPC.

    **Note:** Replace the download URL in the commands with the URL for the region in which the Java application is located.

    -   Download Supervisor from the Internet

        ```
        wget http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsSupervisor.zip -O ArmsSupervisor.zip
        unzip ArmsSupervisor.zip
        ```

    -   Download Supervisor from VPC \(when the Internet download URL is unavailable\)

        ```
        wget http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/ArmsSupervisor.zip -O ArmsSupervisor.zip
        unzip ArmsSupervisor.zip
        ```

2.  Run the following command to modify the name of the Java application:

    ```
    cd ArmsSupervisor
    ./attach.sh </path/to/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar> <PID> <NewAppName> <LicenseKey>
    ```

    -   </path/to/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar\>: the path of the arms-bootstrap-1.7.0-SNAPSHOT.jar file.
    -   <PID\>: the ID of the process. You can run the `jps/ps` command to obtain the version ID.
    -   <NewAppName\>: the new application name.
    -   <LicenseKey\>: the license key of the application monitored by ARMS, which can be obtained from the ARMS console.

If the standard output shown in the following figure is displayed, it indicates that the application name is modified.

[\[Back to the top\]](#sc_toc)

## How do I modify the name of a common Java application on which the ARMS agent is installed with one click?

If you install the ARMS agent with one click, the agent is installed in the ~/.arms/supervisor/agent directory. Note that the account you use must be the same as the application account.

Perform the following steps to modify your application name:

1.  Log on to the machine where the application is located and run the following command:

    ```
    cd ~/.arms/supervisor
    ./cli.sh <LicenseKey> <NewAppName>
    ```

    -   <LicenseKey\>: LicenseKey of the application monitored by ARMS, which can be obtained from the ARMS console.
    -   <NewAppName\>: new application name.
2.  Select the proper process from all Java processes.

    **Note:** If only one process is available, this process is selected by default.

3.  Open the ~/.arms/attach.info file, change the application name to the new name, and save the file.

    **Warning:** Do not add content such as spaces when you modify the file. Otherwise, the modification may fail because it does not match the new application name modified in the preceding steps.

    Wait a moment after your application name is modified. Monitoring data of the application is reported using the new name rather than the previous name.


## How do I change the name of a Java application deployed on ECS instances?

If your Java application is deployed on an ECS instance, the ARMS agent directory is /.arms/agent.

Perform the following steps to modify your application name:

1.  Log on to the ECS instance where your application is located and run the following command with the root account:

    ```
    su <USER> -c "./attach.sh /.arms/agent/arms-bootstrap-1.7.0-SNAPSHOT.jar <PID> <NewAppName> <LicenseKey>"
    ```

    -   <PID\>: target process ID, which can be obtained by using the `jps/ps` command.
    -   <NewAppName\>: new application name.
    -   <LicenseKey\>: LicenseKey of the application monitored by ARMS, which can be obtained from the ARMS console.
2.  Open the ~/.arms/attach.info file, change the application name to the new name, and save the file.

    **Warning:** Do not add content such as spaces when you modify the file. Otherwise, the modification may fail because it does not match the new application name modified in the preceding steps.


If the standard output shown in the following figure is displayed, it indicates that the application name is modified.

## How do I modify the name of a Java application deployed in an ACK cluster?

You can check the version of the ARMS agent by viewing the Version file in the directory of the agent. For example, `2.5.8_cf020486_20190816150025` indicates that the version of the ARMS agent is 2.5.8 and was released on August 16, 2019.

-   If the version of the ARMS agent is earlier than 2.5.8.1, uninstall the agent and install it again. You can specify a new application name when you reinstall the agent.
    -   For more information about how to uninstall the ARMS agent that is manually installed, see[How do I uninstall the ARMS agent that is manually installed?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-2je-5ub-m2q)
    -   For more information about how to uninstall the ARMS agent that is installed with one click, see[How do I uninstall the ARMS agent that is installed with one click?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-lcu-dvl-fyl)
    -   For more information about how to uninstall the ARMS agent installed on applications in ECS instances, see[How do I uninstall the ARMS agent installed on applications in ECS instances?](https://www.alibabacloud.com/help/doc-detail/162776.htm#section-2f1-20j-xgy)
-   If the version of the ARMS agent is 2.5.8.1 or later, you can perform the following steps to modify the name of the Java application without reinstalling the ARMS agent.

    **Note:** ARMS agents downloaded after August 20, 2019 support this feature.


Change the value of the armsPilotCreateAppName parameter in Deployment and restart the pod.

Wait a moment after your application name is modified. Monitoring data of the application is reported using the new name rather than the previous name.

[\[Back to the top\]](#sc_toc)

## How do I modify the name of a Java application deployed in Enterprise Distributed Application Service \(EDAS\)?

The names of Java applications deployed in EDAS cannot be modified.

[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent that is manually installed?

For more information about how to manually install the ARMS agent on Java applications, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md). You can perform the following steps to uninstall the ARMS agent that is manually installed:

1.  If you no longer want to use ARMS to monitor your Java applications, delete all parametersrelated to AppName and LicenseKey, which are described in [Step 8](https://www.alibabacloud.com/help/zh/doc-detail/63797.htm#step-dv3-vvr-lxd).

2.  Restart the Java application.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent that is installed with one click?

For more information about how to install the ARMS agent with one click, see [Install the ARMS agent for a Java application by using scripts](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application by using scripts.md). You can perform the following steps to uninstall the ARMS agent that is installed with one click:

1.  If you no longer want to use ARMS to monitor your Java applications, run the `jps -l` command to view all processes and find the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` in the returned results.

    In this example, the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` is 62857.

    ![Kill Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4872485951/p43111.png)

2.  Run the `kill -9 <process ID>` command.

    Example: `kill -9 62857`.

3.  Run the `rm -rf /.arms /root/.arms` command.

4.  Restart your application.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a Java application deployed on an ECS instance?

1.  If you no longer want to use ARMS to monitor your Java applications, run the `jps -l` command to view all processes and find the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` in the returned results.

    In this example, the process ID of `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` is 62857.

    ![Kill Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4872485951/p43111.png)

2.  Run the `kill -9 <process ID>` command.

    Example: `kill -9 62857`.

3.  Run the `rm -rf /.arms /root/.arms` command.

4.  Restart your application.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a Java application in an ACK cluster?

If you no longer want to use ARMS to monitor your Java applications in an ACK cluster, perform the following steps to uninstall the ARMS agent:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**. On the **Clusters** page, click **Applications** in the **Actions** column corresponding to the cluster that contains the Java application from which you want to uninstall the ARMS agent.

3.  In the left-side navigation pane, select Releases.

4.  On the Helm tab, select the release name **arms-pilot** of the ARMS agent, and click **Delete** in the **Actions** column.

5.  In the Delete dialog box, click **OK**.

6.  Restart your business pod.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a Java application in an open-source Kubernetes environment?

1.  If you no longer want to use ARMS to monitor your Java applications in an open-source Kubernetes environment, run the following command to uninstall arms-pilot:

    ```
    helm del --purge arms-pilot
    ```

2.  Restart your business pod.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a Java application in Docker?

1.  If you no longer want to use ARMS to monitor your Java applications in a Docker cluster, delete the Dockerfile content edited in [Step 1](/intl.en-US/Application monitoring/Start monitoring Java applications/Install the ARMS agent for a Java application deployed in a Docker cluster.md) in the "Install the ARMS agent for applications in Docker" topic.

2.  Run the docker build command to construct the image.

3.  Run the docker run command to start the image.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a PHP application?

If you no longer want to use ARMS to monitor your PHP applications that are not deployed in an ACK cluster, perform the following steps to uninstall the ARMS agent:

1.  Delete the following four lines from the php.ini file:

    ```
    [arms] 
    extension=<php_extension_dir>/arms.so
    arms.trace_exception=true
    arms.config_full_name=/<php-agent-dir>/arms-agent.conf                  
    ```

2.  Restart your PHP application.


[\[Back to the top\]](#sc_toc)

## How do I uninstall the ARMS agent installed on a PHP application in an ACK cluster?

If you no longer want to use ARMS to monitor your PHP applications that are deployed in an ACK cluster, perform the following steps to uninstall the ARMS agent:

1.  Log on to the [Alibaba Cloud Container Service for Kubernetes console](https://cs.console.aliyun.com/#/k8s/overview).

2.  In the left-side navigation pane, click **Clusters**. On the **Clusters** page, click **Applications** in the **Actions** column corresponding to the cluster that contains the Java application from which you want to uninstall the ARMS agent.

3.  In the left-side navigation pane, select Releases.

4.  On the Helm tab, select the release name **arms-pilot** of the ARMS agent, and click **Delete** in the **Actions** column.

5.  In the Delete dialog box, click **OK**.

6.  Restart your business pod.


[\[Back to the top\]](#sc_toc)

## What do I do if the data of my application with the OpenFeign component is incomplete in ARMS?

After your application with the OpenFeign component is connected to ARMS application monitoring, if the data is incomplete and the data of downstream applications cannot be viewed, this may be because that the OpenFeign component enables Hystrix using the RxJava asynchronous framework by default, whereas ARMS does not support asynchronous frameworks.

**Note:** This topic applies to scenarios where the version of the ARMS agent for Java applications is earlier than 2.6.0. The ARMS agent for Java applications of the 2.6.0 version or later already supports asynchronous frameworks.

You can disable Hystrix and enable the OkHttp request class to resolve this problem.

1.  Add the following dependencies to the pom.xml file.

    ```
    <! -- OK Http supports Feign -->
    <dependency>
        <groupId>io.github.openfeign</groupId>
        <artifactId>feign-okhttp</artifactId>
    </dependency>                
    ```

2.  Add the following content to the SpringCloud configuration file:

    ```
    feign.okhttp.enabled: true
    feign.hystrix.enabled: false                 
    ```

3.  Configure the OkHttp request class.

    ```
    @Configuration
    @ConditionalOnClass(Feign.class)
    @AutoConfigureBefore(FeignAutoConfiguration.class)
    public class FeignClientOkHttpConfiguration {
    
        @Bean
        public OkHttpClient okHttpClient() {
            return new OkHttpClient.Builder()
                    // The connection times out.
                    .connectTimeout(20, TimeUnit.SECONDS)
                    // The response times out.
                    .readTimeout(20, TimeUnit.SECONDS)
                    // The write request times out.
                    .writeTimeout(20, TimeUnit.SECONDS)
                    // Indicates whether to enable automatic reconnection.
                    .retryOnConnectionFailure(true)
                    // The connection tool.
                    .connectionPool(new ConnectionPool())
                    .build();
        }                
    ```


[\[Back to the top\]](#sc_toc)

