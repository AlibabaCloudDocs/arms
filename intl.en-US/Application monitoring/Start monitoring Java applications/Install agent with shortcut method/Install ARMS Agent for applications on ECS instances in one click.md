# **Install ARMS Agent for applications on ECS instances in one click** {#concept_109296_zh .concept}

You can use ARMS to monitor the topology, API requests, abnormal and slow transactions, and SQL analysis of applications on ECS instances. This topic describes how to access applications on ECS instances with one click in the ARMS console.

## Prerequisites {#section_zbs_pcj_ygb .section}

-   You have [purchased an ECS instance](https://ecs-buy.aliyun.com/) and deployed an application in the target region.

## Procedure {#section_xqy_wdj_ygb .section}

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home). In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.
2.  On the Applications page that appears, click **Create Application** in the upper-right corner.
3.  On the Create Application page that appears, click the **Batch Install for ECS** tab. When ARMS accesses the ECS instance for the first time, you need to grant ARMS the permission to access the ECS instance. Perform the following steps with the primary account:

    1.  In the dialog box that appears, click **Go to RAM to Authorize**.

    2.  On the Cloud Resource Access Authorization page, select **AliyunARMSAccessingECSRole** and then click **Confirm Authorization Policy**.
    3.  On the Sync ECS page, click Close.

        **Note:** If you want to access ECS applications through a custom monitoring job, synchronize the ECS instance according to [Manage ECS Data Source](https://www.alibabacloud.com/help/doc-detail/42906.htm).

    After performing authorization, go to the Batch Install for ECS tab page. All ECS instances under this primary account are displayed on the ECS Batch Install tab page.

4.  On the Batch Install for ECS tab page, locate the row that contains the target ECS instance, and click **Install Probe** in the **Actions** column. In the **Note** dialog box that appears, click **OK**.

    After ARMS Agent is installed on the ECS instance, ARMS Agent obtains all the processes that run on the ECS instance and displays the processes in the process list below the target ECS instance.

    **Note:** If processes that run on the ECS instance are incorrect after ARMS Agent is installed, click **-** and then **+** at the left of the ECS instance to refresh the page. If ARMS Agent cannot be installed, see [FAQ](#section_wqk_sxc_zgb) for the solution.

5.  After ARMS Agent is installed, in the following dialog box, locate the row that contains the target process, edit the application name, and then click **Start Application Monitoring** in the **Actions** column.

    **Note:** When the application names of multiple processes are the same, they appear as multiple instances under the same application monitoring job.


After one minute, if your application is displayed in the application list and has data reported, your application has been connected to ARMS.

## Uninstall ARMS Agent {#section_l2f_wvc_zgb .section}

When you no longer need to monitor applications on an ECS instance, you can uninstall ARMS Agent from the ECS instance. After ARMS Agent is uninstalled, ARMS stops monitoring all the processes of the ECS instance. You can uninstall ARMS Agent as follows:

1.  On the ECS instance in which ARMS Agent is installed, run the `jps -l` command to view all the processes. In the results returned, locate `com.alibaba.mw.arms.apm.supervisor.daemon.Daemon` and view the process number.

    In this example, the process number is 62857.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152233/156783525443111_en-US.png)

2.  Run the command `kill -9 process number`, for example, `kill -9 62857`.

3.  Restart your application.

## FAQ {#section_wqk_sxc_zgb .section}

What should I do when ARMS Agent cannot be installed?

1.  Make sure that your ECS instance can access the ARMS Agent download link in the region of your instance.

    ``` {#codeblock_95b_vpy_mtz}
    Make sure that your ECS instance can access the Internet and download ARMS Agent on the One-click Access to Java Applications page.
    
    # China (Hangzhou)
    http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/install.sh
    # China (Shanghai)
    http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/install.sh
    # China (Qingdao)
    http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/install.sh
    # China (Beijing)
    http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/install.sh
    # China (Shenzhen)
    http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/install.sh
    # Singapore
    http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/install.sh
    					
    ```

2.  Make sure that your ECS instance can access the ARMS console.

    ``` {#codeblock_n3o_nov_uou}
    
    #Mainland China
    https://arms.console.aliyun.com/
    
    #Singapore
    https://arms-ap-southeast-1.console.aliyun.com
    ```

3.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) and check the following items.
    1.  In the left-side navigation pane, choose **Cloud Assistant**.
    2.  On the Cloud Assistant page that appears, enter the command `InstallJavaAgent` in the search box.

        **Note:** If no result is returned, contact Customer Services of ARMS.

    3.  In the **Tasks** section, enter the ID of the command `InstallJavaAgent` in the search box. In the result that is returned, locate the row that contains the target record and click **View Results** in the **Actions** column to check whether the `InstallJavaAgent` command has run. If it has failed to run, troubleshoot the problem according to the execution result details. If the problem is caused because the ECS disk is full or ARMS Java Agent is not installed, you can clear the disk or install ARMS Java Agent to solve the problem. If you cannot solve the problem by yourself, send the detailed execution results to ARMS Customer Services.

## References {#section_gr2_ds2_zgb .section}

-   [Install ARMS Agent for applications on ECS instances with one click](../../../../intl.en-US/FAQ/Application Monitoring FAQ/Install ARMS Agent for applications in ECS with one click.md#)

