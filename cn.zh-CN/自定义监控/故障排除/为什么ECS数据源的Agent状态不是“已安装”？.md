---
keyword: [ECS数据源, Agent状态]
---

# 为什么ECS数据源的Agent状态不是“已安装”？

本文介绍ECS数据源的Agent状态非“已安装”情况的解决办法。

## Condition

ECS数据源的Agent状态不是“已安装”。

## Cause

Agent运行异常、ARMS未授权、或Logtail配置中的地域（Region）与机器所在地域不一致都有可能导致ECS数据源的Agent状态非“已安装”。

## Remedy

1.  检测Agent（Logtail）是否运行正常。

    ```
    sudo /etc/init.d/ilogtaild status
    ```

    -   如果状态不是`running`，则说明Logtail安装不正确，请重新安装Logtail。
        1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。
        2.  在左侧导航栏中选择**自定义监控数据源管理** \> **云服务器ECS**。
        3.  在**云服务器ECS**页签上，单击目标实例**操作**列中的**安装Agent**，并按照对话框中的提示逐步操作。
    -   如果状态是`running`，则继续执行[步骤2](#step_ej7_wj7_0w0)。
2.  检查是否已为ARMS授权。

    ```
    ls /etc/ilogtail/users/1098370038733503
    ```

    -   如果最初安装Logtail之后没有为ARMS授权，则执行以下授权操作。

        ```
        sudo touch /etc/ilogtail/users/1098370038733503
        ```

    -   如果已授权，则继续执行[步骤3](#step_s0v_69d_6wn)。
3.  检查Logtail配置中的地域（Region）与机器所在地域是否一致。

    ```
    cat /usr/local/ilogtail/ilogtail_config.json
    ```

    例如，以下示例Logtail配置中的接入地域为**cn-hangzhou**。

    ```
    {
      "config_server_address" : "http://logtail.cn-hangzhou-intranet.log.aliyuncs.com",
      "data_server_list" :
      [
        {
          "cluster" : "cn-hangzhou",
          "endpoint" : "cn-hangzhou-intranet.log.aliyuncs.com"
        }
      ],
      "cpu_usage_limit" : 0.4,
      "mem_usage_limit" : 200,
      "max_bytes_per_sec" : 2097152,
      "bytes_per_sec" : 1048576,
      "buffer_file_num" : 25,
      "buffer_file_size" : 20971520,
      "buffer_map_num" : 5,
      "streamlog_open" : false,
      "streamlog_pool_size_in_mb" : 50,
      "streamlog_rcv_size_each_call" : 1024,
      "streamlog_formats": [],
      "streamlog_tcp_port" : 11111
    }
    ```

    -   如果当前ECS的地域与Logtail配置不一致，则可以确定是Logtail下载或者安装错误，请按照正确的地域重新下载和安装Logtail。
    -   如果当前ECS的地域与Logtail配置一致，则继续执行[步骤](#step_bos_d5n_slt)[4](#step_bos_d5n_slt)。
4.  检查实际上报SLS服务端的IP地址是否为ECS的私网IP地址。

    ```
    cat /usr/local/ilogtail/app_info.json
    ```

    例如，在以下示例的应用Info文件中，ip即为实际上报SLS服务端的IP地址。

    ```
    {
      "UUID" : "<yourAppId>",
      "hostname" : "<yourHostName>",
      "ip" : "192.168.XX.XX"
      "logtail_version": "0.13.4",
      "os" : "Linux; 3.10.0-514.26.2.el7.x86_64; #1 SMP Tue Jul 4 15:04:05 UTC 2017; x86_64",
      "update_time" : "2017-08-30 22:54:55"
    }
    ```

    ![ECS Private IP](../images/p43208.png "示例：ECS的私网IP")

    -   如果该IP地址与ECS的私网IP地址不一致，则执行以下命令。

        ```
        cat /etc/hosts
        hostname -i
        ```

        **说明：** 如果本机在/etc/hosts文件中设置了主机名绑定，则需要确认绑定的IP地址。执行hostname命令可查看主机名。如果没有设置主机名绑定，则会自动识别本机第一块网卡的IP地址。

    -   如果该IP地址与ECS的私网IP地址一致，则联系ARMS钉钉服务账号：arms160804。

