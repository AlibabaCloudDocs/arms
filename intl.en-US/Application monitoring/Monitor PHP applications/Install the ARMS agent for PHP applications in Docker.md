---
keyword: [PHP, Application Monitoring, Docker]
---

# Install the ARMS agent for PHP applications in Docker

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a PHP application deployed in Docker, you can use it to monitor the PHP application. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis. This topic describes how to install the ARMS agent for a PHP application in Docker.

## Procedure

1.  Run the Docker container on the host where the ARMS agent needs to be installed.

    ```
    sudo docker run -d -p 11234:11234 <IMAGE>
    ```

    You must replace `<IMAGE>` with the following addresses based on regions.

    |Region|Download URL|
    |------|------------|
    |China \(Hangzhou\)|    ```
registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Shanghai\)|    ```
registry.cn-shanghai.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Qingdao\)|    ```
registry.cn-qingdao.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Beijing\)|    ```
registry.cn-beijing.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Zhangjiakou-Beijing Winter Olympics\)|    ```
registry.cn-zhangjiakou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Shenzhen\)|    ```
registry.cn-shenzhen.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |China \(Hong Kong\)|    ```
registry.cn-hongkong.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |Singapore \(Singapore\)|    ```
registry.ap-southeast-1.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |

    **Note:** In this case, port 11234 of the host exposes the Hercules service. If a port conflict occurs, map port 11234 to another port of the host.

2.  Select the Internet or Virtual Private Cloud \(VPC\) download URL based on your network environment. For more information, run the `Wget` command to download the agent installation package.

    The following table lists the download URLs on the Internet.

    |Region|Download URL|
    |------|------------|
    |China \(Hangzhou\)|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shanghai\)|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Qingdao\)|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Beijing\)|    ```
wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Zhangjiakou-Beijing Winter Olympics\)|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shenzhen\)|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Hong Kong\)|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Singapore \(Singapore\)|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Regions for Alibaba GovCloud|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |

    The following table lists the download URLs in VPC environments.

    |Region|Download URL|
    |------|------------|
    |China \(Hangzhou\)|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shanghai\)|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Qingdao\)|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Beijing\)|    ```
wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Zhangjiakou-Beijing Winter Olympics\)|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shenzhen\)|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Hong Kong\)|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Singapore \(Singapore\)|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Regions for Alibaba GovCloud|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |

3.  Decompress the installation package and move it to the /usr/local/arms/arms-php-agent directory.

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

4.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. At the top of the Applications page, select a region as required. On the page that appears, click **Add Application** in the upper-right corner.

5.  Copy LicenseKey at the top of the Add Application page.

6.  Add the following content to the php.ini file:

    ```
    extension=/usr/local/arms/arms-php-agent/arms-x.x.so
    [ARMS]
    arms.enable=1
    arms.app_name=<yourAppName>
    arms.license_key=<yourLicenseKey>
    arms.network_type=tcp
    arms.tcp_host=<host>
    arms.tcp_port=<port>
    ```

    **Note:**

    -   `x.x` in `arms-x.x.so` is the version of your PHP application. Versions 5.4 to 7.3 are supported.
    -   If your container image system is an Alpine Linux system, change `arms-[x.x].so` to `arms-[x.y]-alpine.so`, where `[x.y]` can be 5.5, 5.6, 7.0, 7.1, 7.2, or 7.3.
    -   Set <yourAppName\> to a custom name. Then, your PHP application name in the ARMS console will be the same as the custom name.
    -   Replace <yourLicenseKey\> with the license key obtained in [Step](#step_2le_9mc_ckc)[5](#step_2le_9mc_ckc).
    -   <host\> and <port\> are respectively the IP address and port number of the host of the container. The default port number is 11234. If the port number is updated in [Step](#step_lyt_uog_s4p)[1](#step_lyt_uog_s4p), update it in this step.
    -   If `with-config-file-scan-dir` is configured for the version of your PHP application, you can create the arms.ini file in the /etc/php/7.2/php-fpm/conf.d directory. The content of this file is the same as that added to the php.ini file.
7.  Add the commands in [Step](#step_k2r_2sb_m0r)[2](#step_k2r_2sb_m0r) to [Step](#step_2hh_ahv_0qw)[6](#step_2hh_ahv_0qw) to the dockerfile file for auto running.

8.  Restart your PHP application.


**Related topics**  


[Before you begin](/intl.en-US/Application monitoring/Preparations.md)

[Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for common PHP applications.md)

