---
keyword: [PHP, application monitoring, Docker]
---

# Install the ARMS agent for a PHP application deployed in a Docker cluster

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a PHP application that is deployed in a Docker cluster, ARMS starts to monitor the PHP application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. This topic describes how to install the ARMS agent for a PHP application that is deployed in a Docker cluster.

**Note:** If you want to use the PHP Agent of the latest version, activate [ARMS trial](https://common-buy.aliyun.com/?&commodityCode=arms#/open) now. For the trial period of the new version of the PHP Agent, visit the ARMS console announcement. If you have other questions, you can join our DingTalk Q&A Group: 23328286.

## Install the ARMS agent for a PHP application deployed in a Docker cluster

1.  Run a Docker container on the host where the ARMS agent needs to be installed.

    ```
    sudo docker run -d -p 11234:11234 <IMAGE>
    ```

    Replace `<IMAGE>` with one of the following download links based on your region.

    |Region|Download link|
    |------|-------------|
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
    |China \(Zhangjiakou\)|    ```
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

2.  Run the `wget` command to download the installation package. Select the download link based on your network environment.

    |Region|Download link for the Internet|Download link for VPC|
    |------|------------------------------|---------------------|
    |China \(Hangzhou\)|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shanghai\)|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Qingdao\)|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Beijing\)|    ```
wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Zhangjiakou\)|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Shenzhen\)|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |China \(Hong Kong\)|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Singapore \(Singapore\)|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |Alibaba Gov Cloud|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |

3.  Decompress the installation package and move it to the /usr/local/arms/arms-php-agent directory.

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

4.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

5.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

6.  On the Applications page, click **Add Application** in the upper-right corner.

7.  Copy the license key at the top of the Add Application page.

8.  Add the following code to the php.ini configuration file:

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
    -   If your container image system is Alpine Linux, change `arms-x.x.so` to `arms-[x.y]-alpine.so`, where `[x.y]` can be 5.5, 5.6, 7.0, 7.1, 7.2, or 7.3.
    -   Set <yourAppName\> to a custom name. The name is displayed as your PHP application name in the ARMS console.
    -   Replace <yourLicenseKey\> with the license key that you obtained in [Step 7](#step_2le_9mc_ckc).
    -   <host\> and <port\> indicate the IP address and port number that are used by the container to access the host. The default port number is 11234. If you update the port number in [Step 1](#step_lyt_uog_s4p), you must also update it in this step.
    -   If `with-config-file-scan-dir` is configured for the version of your PHP application, you can create the arms.ini file in the /etc/php/7.2/php-fpm/conf.d directory. The content of this file is the same as that you added to the php.ini file.
9.  Add the commands in [Step 2](#step_k2r_2sb_m0r) to Step 8 to the dockerfile file for auto running.

10. Restart your PHP application.


**Related topics**  


[Before you begin]()

[Install the ARMS agent for a PHP application](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for a PHP application.md)

