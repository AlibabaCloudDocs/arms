# 为 PHP 应用安装探针 {#concept_102783_zh .concept}

为 PHP 应用安装 ARMS 探针并重启应用后，ARMS 即可对 PHP 应用进行应用拓扑、调用链路追踪、异常事务和慢事务监控、SQL 分析等一系列监控。

## 前提条件 {#section_rgl_qs1_mgb .section}

-   确保您使用的公网服务器安全组已开放 8442、8443、8883 三个端口的 TCP 公网出方向权限，VPC 内不需要开通。为阿里云 ECS 开放出方向权限，请参见[添加安全组规则](../../../../intl.zh-CN/安全/安全组/添加安全组规则.md#)。

    **说明：** ARMS 不仅可接入阿里云 ECS 上的应用，还能接入其他能访问公网的服务器上的应用。

-   确保您的应用使用的第三方组件或框架在应用监控兼容性列表范围内，请参见[应用监控兼容性列表](intl.zh-CN/应用监控/参考信息/应用监控兼容性列表.md#)。


## 接入 PHP 探针 {#section_ndm_0ma_dvl .section}

1.  登录 [ARMS 控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表** 。
2.  在应用列表页面右上角单击**新接入应用**。

3.  在新接入应用页面选择使用语言为 **PHP**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152237/156750362444408_zh-CN.png)

4.  采用以下任意一种方法下载 PHP 探针，完成后单击**下一步**。

    -   方法一：手动下载。单击**下载探针**按钮，下载最新 ZIP 包。

    -   方法二：Wget 命令下载。根据所在地域使用 Wget 命令下载 Agent 压缩包。

    ``` {#codeblock_uzh_35c_45o}
    # 杭州地域
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 上海地域
    wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 青岛地域
    wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 北京地域
    wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 深圳地域
    wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 新加坡地域
    wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    
    # 金融云环境
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/arms-php-agent.zip" -O arms-php-agent.zip
    					
    ```

5.  切换到安装包所在目录，运行以下命令解压安装包到任意工作目录下。

    ``` {#codeblock_7cw_45q_dig}
    unzip arms-php-agent.zip /{user.workspace}/
    ```

    **说明：** `{user.workspace}` 是示例路径，请按需修改。

6.  在安装探针页签查看并保存 LicenseKey。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152237/156750362443126_zh-CN.png)

7.  采用以下方法之一安装和配置探针。

    -   自动安装。执行以下命令自动安装探针。

        ``` {#codeblock_4uh_3lp_742}
        cd arms-php-agent 
        ./install.sh <licenseKey> PHP-Demo                     
        ```

        **说明：** 

        -   将 `<licenseKey>` 替换为您的 LicenseKey。
        -   将 PHP-Demo 替换成您的应用名称。应用名称暂不支持中文字符。
    -   手动安装。

        1.  切换到探针解压目录。

            ``` {#codeblock_9nf_ltv_y5p}
            cd arms-php-agent                                 
            ```

        2.  修改 arms-agent.conf 文件中的配置项。

            ``` {#codeblock_afq_eep_r1t}
            LicenseKey=<licenseKey>
            AppName=PHP-Demo
            PluginRootDir=<arms-php-agent>                            
            ```

            **说明：** 

            -   将 `<licenseKey>` 替换为您的 LicenseKey。
            -   将 PHP-Demo 替换成您的应用名称。应用名称暂不支持中文字符。
            -   将 `<arms-php-agent>` 替换为解压后 arms-php-agent 目录下 plugins 的绝对路径。
        3.  执行以下命令获取 PHP 拓展安装目录。

            ``` {#codeblock_8sf_b40_qak}
            php -i | grep ^extension_dir                               
            ```

            若返回结果如下所示，则安装目录为 `/usr/lib/php/extensions/no-debug-non-zts-20160303`。

            ``` {#codeblock_y4t_dyj_zr0}
            extension_dir => /usr/lib/php/extensions/no-debug-non-zts-20160303 => /usr/lib/php/extensions/no-debug-non-zts-20160303                  
            ```

        4.  将 arms.so 文件拷贝到上一步获取的 PHP 拓展安装目录。

            ``` {#codeblock_gyc_rf4_4hq}
            sudo cp arms.so /usr/lib/php/extensions/no-debug-non-zts-20160303                  
            ```

        5.  新增动态链接库路径。

            ``` {#codeblock_x6p_nkn_m0a}
            sudo vi /etc/ld.so.conf                      
            ```

        6.  新增动态链接共享库和静态档案库。

            ``` {#codeblock_c7r_znb_00u}
            <php-agent-dir>/lib                           
            ```

            **说明：** `<php-agent-dir>` 为探针解压后的绝对路径。

        7.  加载动态链接库。

            ``` {#codeblock_mjg_vy0_zk4}
            sudo ldconfig                                   
            ```

8.  在 php.ini 文件末尾添加以下内容 。

    ``` {#codeblock_so0_9mi_6c8}
    [arms]
    extension=<php_extension_dir>/arms.so
    arms.trace_exception=true
    arms.config_full_name=/<php-agent-dir>/arms-agent.conf        
    ```

    **说明：** 

    -   若使用脚本安装，请使用脚本提示的替换内容。
    -   若使用手动安装，则需将 `<php_extension_dir>` 替换为 PHP 拓展安装目录，默认安装目录为 `/usr/lib64/xxx`，`<php-agent-dir>` 替换为解压后探针目录的绝对路径。
9.  重启您的 PHP 应用。


## 结果验证 {#section_sgf_wn5_tj9 .section}

约一分钟后，若您的 PHP 应用出现在应用列表中且有数据上报，则说明接入成功。

## 卸载 PHP 探针 {#section_iip_fk5_0ej .section}

当您不需要 ARMS 监控 PHP 应用时，可按照以下步骤卸载探针。

1.  修改 php.ini 文件，删除以下四行：

    ``` {#codeblock_y4w_x5u_qnb}
    [arms] 
    extension=<php_extension_dir>/arms.so
    arms.trace_exception=true
    arms.config_full_name=/<php-agent-dir>/arms-agent.conf                  
    ```

2.  重启您的 PHP 应用。


卸载探针后，您的应用数据将不会上报 ARMS。

