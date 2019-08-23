# Install ARMS Agent for applications in ECS with one click {#concept_109300_zh .concept}

This topic lists FAQ about installing ARMS Agent for applications in EDAS with one click, and provides solutions.

## What should I do when ARMS Agent cannot be installed? {#section_wqk_sxc_zgb .section}

1.  Make sure that your ECS instance can access the ARMS Agent download link in the region of your instance.

    ``` {#codeblock_g31_s2g_qas}
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

    ``` {#codeblock_wdg_na7_syu}
    
    #Mainland China
    https://arms.console.aliyun.com/
    
    #Singapore
    https://arms-ap-southeast-1.console.aliyun.com
    ```

3.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) and check the following items:
    1.  In the left-side navigation pane, choose **Cloud Assistant**.
    2.  On the Cloud Assistant page that appears, select Command in the search box, and enter the `InstallJavaAgent` command.

        **Note:** If no result is returned, contact Customer Services of ARMS.

    3.  In the **Tasks** section, enter the ID of the `InstallJavaAgent` command in the search bar. In the results that are returned, locate the row that contains the target record and click **View Results** in the **Actions** column to check whether the `InstallJavaAgent` command has run. If not, troubleshoot the problem based on the detailed execution results \(for example, the ECS disk is full, and ARMS Java Agent is not installed\). If the problem persists, submit the detailed execution results to Customer Services of ARMS.

## Why is the ECS instance process information inaccurate after ARMS Agent has been installed? {#section_kui_kc1_9ap .section}

After you install ARMS Agent, if no ECS instance process information is displayed or the ECS instance process information is inaccurate, click **-** and then **+** on the left of the ECS instance. If the problem persists, contact Customer Services of ARMS.

## What should I do if I cannot enable ARMS for a process on the ECS instance? {#section_czz_vr2_zgb .section}

On the ECS instance, check whether the `/.arms/supervisor/logs/arms-supervisor.log` file contains error logs. If it does, troubleshoot the problem according to the error message. If the problem persists, contact Customer Services of ARMS.

