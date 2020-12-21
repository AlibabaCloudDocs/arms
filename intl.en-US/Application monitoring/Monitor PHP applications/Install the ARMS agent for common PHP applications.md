---
keyword: [PHP, Application monitoring, Performance monitoring]
---

# Install the ARMS agent for common PHP applications

After installing the application real-time Monitoring Service \(ARMS\) PHP agent, you can monitor PHP applications. For example, you can view the monitoring data of application topology, traces, abnormal transactions, and slow transactions, and conduct SQL analysis. The new version of the ARMS agent for PHP has deeply optimized the application performance. ARMS can reduce the CPU and memory usage of the agent to about 5%.

## Install the ARMS agent for common PHP applications

1.  Select the public network download address or VPC download address based on your network environment, and use the Wget command to download the compressed installation package.

    The following figure shows the download URLs in the public network.

    ```
    # China (Hangzhou)
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Shanghai)
    wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Qingdao)
    wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Beijing)
    wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Zhangjiakou)
    wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Shenzhen)
    wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Hong Kong)
    wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    ```

    The following figure shows the download link in the VPC.

    ```
    # China (Hangzhou)
    wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Shanghai)
    wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Qingdao)
    wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Beijing)
    wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Zhangjiakou)
    wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Shenzhen)
    wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    # China (Hong Kong)
    wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/grey/arms-php-agent.zip" -O arms-php-agent.zip
    ```

2.  Run the following command to extract and move the installation package to /usr/local/arms/arms-php-agent table of contents

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

3.  In the left-side navigation pane, choose **application monitoring** \> **application List**, and in application List at the top of the page, select the target region, and in the upper-right corner, click **application Access**.

4.  In application Access copy LicenseKey at the top of the page.

5.  In php.ini add the following code to the configuration file.

    ```
    extension=/usr/local/arms/arms-php-agent/arms-x.x.so
    [ARMS]
    arms.enable=1
    arms.app_name=<yourAppName>
    arms.license_key=<yourLicenseKey>
    arms.sock_path=/arms.sock
    ```

    **Note:**

    -   `arms-x.x.so` in `x.x` the version of your PHP application. Currently, PHP applications of versions 5.4 to 7.3 are supported.
    -   Customize Settings `<yourAppName>`, which will display your PHP application in the ARMS console.
    -   Will `<yourLicenseKey>` replace with [step](#step_uz0_rqc_n3i)[4](#step_uz0_rqc_n3i) the LicenseKey.
    -   If the corresponding version of your PHP application is configured with `with-config-file-scan-dir`, you can /etc/php/7.2/php-fpm/conf.d create a new item in the directory arms.ini file, content and above in php.ini the content added in the file is consistent.
6.  Run the following command to start Hercules and report your PHP application data.

    ```
    cd /usr/local/arms/arms-php-agent/
    sudo ./hercules service install
    sudo ./hercules service start
    ```

7.  Restart the service.

    -   If you are using an Ngnix server, restart the PHP-FPM.
    -   If you are using the Apache server, restart Apache2 service.

## Uninstall the ARMS agent

1.  Delete [step](#step_spb_vdc_0nq)[5](#step_spb_vdc_0nq) added in php.ini file content or arms.ini file.

2.  Restart the service.

    -   If you are using an Ngnix server, restart the PHP-FPM.
    -   If you are using the Apache server, restart Apache2 service.
3.  Run the following commands to stop and uninstall the Hercules service:

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

4.  Run the following command to delete the arms Agent Directory:

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    You have completely uninstalled ARMS PHP agent.


**Related topics**  


[Install the ARMS agent for PHP applications deployed on multiple servers in standalone mode](/intl.en-US/Application monitoring/Monitor PHP applications/Install the arms agent for multi-site and standalone PHP applications.md)

