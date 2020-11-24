---
keyword: [PHP, 应用监控, 性能监控]
---

# 为普通PHP应用安装探针

为PHP应用安装ARMS PHP探针后，ARMS即可开始监控PHP应用，您可以查看应用拓扑、调用链路、异常事务、慢事务和SQL分析等一系列监控数据。与此同时，ARMS提供的新版PHP探针，在性能方面进行深度优化，可将探针对CPU及内存的占用率控制在5%左右。

**说明：** 如果您需要试用新版PHP Agent，请立即开通[ARMS试用版](https://common-buy.aliyun.com/?&commodityCode=arms#/open)。新版PHP Agent的试用期结束时间请参见ARMS控制台公告。若您还有其他问题，可加入我们的钉钉答疑群：23328286。

1.  使用**Wget**命令下载。根据您的地域下载对应的Agent安装包。

    |地域|公网地址|VPC地址|
    |--|----|-----|
    |华东1（杭州）|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |华东2（上海）|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |华北1（青岛）|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |华北2（北京）|    ```
wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |华北3（张家口）|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |华南1（深圳）|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |中国（香港）|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |

2.  执行以下命令，将安装包解压并移动至/usr/local/arms/arms-php-agent目录。

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

3.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

4.  在左侧导航栏中选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

5.  在应用列表页面右上角单击**接入应用**。

6.  在接入应用页面顶部复制的LicenseKey。

7.  在php.ini配置文件中添加以下内容。

    ```
    extension=/usr/local/arms/arms-php-agent/arms-x.x.so
    [ARMS]
    arms.enable=1
    arms.app_name=<yourAppName>
    arms.license_key=<yourLicenseKey>
    arms.sock_path=/arms.sock
    ```

    **说明：**

    -   `arms-x.x.so`中的`x.x`为您的PHP应用的版本，目前支持5.4~7.3版本的PHP应用。
    -   自定义设置`<yourAppName>`，您的PHP应用会以此名称显示在ARMS控制台中。
    -   将`<yourLicenseKey>`替换为[步骤](#step_uz0_rqc_n3i)获取的LicenseKey。
    -   如果您的PHP应用对应的版本配置了`with-config-file-scan-dir`，则可在/etc/php/7.2/php-fpm/conf.d目录下新建arms.ini文件，内容与以上在php.ini文件中添加的内容一致。
8.  执行以下命令，启动Hercules服务上报您的PHP应用数据。

    ```
    cd /usr/local/arms/arms-php-agent/
    sudo ./hercules service install
    sudo ./hercules service start
    ```

9.  重启服务。

    -   如果您使用的是Ngnix服务器，则重启PHP-FPM服务。
    -   如果您使用的是Apache服务器，则重启Apache2服务。
    等待1分钟左右，如果[ARMS控制台](https://arms-intl.console.aliyun.com/)的**应用监控** \> **应用列表**页面上出现了您的应用（应用名称为自定义的<yourAppName\>），则说明您已成功安装探针。


## 卸载探针

1.  删除[步骤](#step_spb_vdc_0nq)中添加的php.ini文件内容或arms.ini文件。

2.  重启服务。

    -   如果您使用的是Ngnix服务器，则重启PHP-FPM服务。
    -   如果您使用的是Apache服务器，则重启Apache2服务。
3.  执行以下命令停止并卸载Hercules服务。

    ```
    sudo ./hercules service stop
    sudo ./hercules service uninstall
    ```

4.  执行以下命令删除探针目录。

    ```
    sudo rm -rf /usr/local/arms/arms-php-agent
    ```

    您已完全卸载ARMS PHP探针。


**相关文档**  


[为单机多站点PHP应用安装探针](/intl.zh-CN/应用监控/开始监控 PHP 应用/为单机多站点PHP应用安装探针.md)

