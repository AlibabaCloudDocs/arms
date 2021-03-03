---
keyword: [PHP, 应用监控, Docker]
---

# 为Docker中的PHP应用安装Agent

为部署在Docker中的PHP应用安装ARMS PHP Agent后，ARMS即可开始监控PHP应用，您可以查看应用拓扑、调用链路、异常事务、慢事务和SQL分析等一系列监控数据。本文介绍如何为Docker中的PHP应用安装Agent。

**说明：** 如果您需要试用新版PHP Agent，请立即开通[ARMS试用版](https://common-buy.aliyun.com/?&commodityCode=arms#/open)。新版PHP Agent的试用期结束时间请参见ARMS控制台公告。若您还有其他问题，可加入我们的钉钉答疑群：23328286。

## 为Docker中的PHP应用安装Agent

1.  在需安装ARMS的机器上运行Docker容器。

    ```
    sudo docker run -d -p 11234:11234 <IMAGE>
    ```

    其中，您需要根据所在地域将`<IMAGE>`替换为以下地址。

    |地域|下载地址|
    |--|----|
    |华东1（杭州）|    ```
registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华东2（上海）|    ```
registry.cn-shanghai.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北1（青岛）|    ```
registry.cn-qingdao.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北2（北京）|    ```
registry.cn-beijing.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华北3（张家口）|    ```
registry.cn-zhangjiakou.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |华南1（深圳）|    ```
registry.cn-shenzhen.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |中国（香港）|    ```
registry.cn-hongkong.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |
    |亚太东南（新加坡）|    ```
registry.ap-southeast-1.aliyuncs.com/arms-docker-repo/arms-hercules:v1.1
    ``` |

    **说明：** 此时，该机器的11234端口暴露了Hercules服务。若出现端口冲突，则将11234端口映射至该机器的其他端口。

2.  根据所处网络环境选择公网下载地址或VPC下载地址，使用`Wget`命令下载Agent压缩安装包。

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
    |亚太东南（新加坡）|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |
    |政务云|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ```

|    ```
wget "http://arms-apm-gov.oss-cn-north-2-gov-1-internal.aliyuncs.com/arms-php-agent.zip" -O arms-php-agent.zip
    ``` |

3.  将安装包解压缩并移动至/usr/local/arms/arms-php-agent目录。

    ```
    unzip arms-php-agent.zip
    mkdir -p /usr/local/arms
    mv arms-php-agent /usr/local/arms/arms-php-agent
    ```

4.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

5.  在左侧导航栏中选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

6.  在应用列表页面右上角单击**接入应用**。

7.  在接入应用页面复制顶部的LicenseKey。

8.  在php.ini配置文件中添加以下内容。

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

    **说明：**

    -   `arms-x.x.so`中的`x.x`为您的PHP应用的版本，目前支持5.4~7.3版本的PHP应用。
    -   若您的容器镜像是Alpine Linux系统，则将`arms-x.x.so`改为`arms-[x.y]-alpine.so`，其中`[x.y]`支持的版本值为5.5、5.6、7.0、7.1、7.2和7.3。
    -   自定义设置<yourAppName\>，您的PHP应用会以此名称显示在ARMS控制台中。
    -   将<yourLicenseKey\>替换为[步骤](#step_2le_9mc_ckc)获取的LicenseKey。
    -   <host\>和<port\>为容器访问主机的IP地址和端口号，端口号默认为11234，若[步骤](#step_lyt_uog_s4p)更新了端口号，此处请同步更新。
    -   如果您的PHP应用对应的版本配置了`with-config-file-scan-dir`，则可在/etc/php/7.2/php-fpm/conf.d目录下新建arms.ini文件，内容与以上在php.ini文件中添加的内容一致。
9.  [步骤](#step_k2r_2sb_m0r)至[步骤](#step_2hh_ahv_0qw)的操作命令可以添加至dockerfile文件自动运行。

10. 重启您的PHP应用。


**相关文档**  


[为普通PHP应用安装探针](/intl.zh-CN/应用监控/接入应用监控/开始监控PHP应用/为普通PHP应用安装探针.md)

