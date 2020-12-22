---
keyword: [PHP, application monitoring, performance monitoring]
---

# Install the ARMS agent for a PHP application

After you install the Application Real-Time Monitoring Service \(ARMS\) agent for a PHP application, ARMS starts to monitor the PHP application. You can view the monitoring data of application topology, API requests, abnormal transactions, slow transactions, and SQL analysis. The performance of the latest ARMS agent is optimized. The CPU and memory usage of the agent is reduced to around 5%.

**Note:** If you want to use the PHP Agent of the latest version, activate [ARMS trial](https://common-buy.aliyun.com/?&commodityCode=arms#/open) now. For the trial period of the new version of the PHP Agent, visit the ARMS console announcement. If you have other questions, you can join our DingTalk Q&A Group: 23328286.

## Install the ARMS agent

1.  Run the **wget** command to download the installation package. Download the installation package based on your region.

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

2.  Run the following command to decompress the installation package and move it to the /usr/local/arms/arms-php-agent directory:

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

3.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

4.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

5.  On the Applications page, click **Add Application** in the upper-right corner.

6.  Copy the license key at the top of the Add Application page.

7.  Add the following code to the php.ini configuration file.

    ```
    extension=/usr/local/arms/arms-php-agent/arms-x.x.so
    [ARMS]
    arms.enable=1
    arms.app_name=<yourAppName>
    arms.license_key=<yourLicenseKey>
    arms.sock_path=/arms.sock
    ```

    **Note:**

    -   `x.x` in `arms-x.x.so` is the version of your PHP application. Versions 5.4 to 7.3 are supported.
    -   Set `<yourAppName>` to a custom name. The name is displayed as your PHP application name in the ARMS console.
    -   Replace `<yourLicenseKey>` with the license key that you obtained in [Step 6](#step_uz0_rqc_n3i).
    -   If `with-config-file-scan-dir` is configured for the version of your PHP application, you can create the arms.ini file in the /etc/php/7.2/php-fpm/conf.d directory. The content of this file is the same as that you added to the php.ini file.
8.  Run the following command to start the Hercules service to transfer the data of your PHP application:

    ```
    cd /usr/local/arms/arms-php-agent/
    sudo ./hercules service install
    sudo ./hercules service start
    ```

9.  Restart the service.

    -   If you are using an NGINX server, restart the PHP-FPM service.
    -   If you are using an Apache server, restart the Apache2 service.
    Wait for about 1 minute. In the [ARMS console](https://arms-intl.console.aliyun.com/), choose **Application Monitoring** \> **Applications** If your application \(with a custom name\) appears on the page, <yourAppName\> you have successfully installed the arms agent.


## Uninstall the ARMS agent

1.  Delete the content of the php.ini or arms.ini file that you added in [Step 7](#step_spb_vdc_0nq).

2.  Restart the service.

    -   If you are using an NGINX server, restart the PHP-FPM service.
    -   If you are using an Apache server, restart the Apache2 service.
3.  Run the following commands to stop and uninstall the Hercules service:

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

4.  Run the following command to delete the directory of the ARMS agent:

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    You have uninstalled the ARMS agent for the PHP application.


**Related topics**  


[Install the ARMS agent for PHP applications deployed on multiple servers in standalone mode](/intl.en-US/Application monitoring/Monitor PHP applications/Install the ARMS agent for PHP applications deployed on multiple servers in standalone
         mode.md)

