# 为Docker中的Java应用安装Agent

为Docker中的Java应用安装ARMS Agent后，ARMS即可开始监控Java应用，且ARMS将自动适配该应用运行的环境，不需要针对Tomcat、Jetty或Spring Boot等应用单独配置运行环境。本文介绍如何为Docker中的Java应用安装Agent。

-   您已开通ARMS，具体操作，请参见[开通和升级ARMS](/cn.zh-CN/快速入门/开通和升级ARMS.md)。
-   您已在Docker中部署Java应用。
-   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，请升级至1.8.X最新版本。


对于Java应用镜像\{original-docker-image:tag\}，可以通过编辑Dockerfile文件来集成已有镜像，然后构建和启动新的镜像，即可将Java应用接入ARMS应用监控。

## 步骤一：获取应用监控License Key

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**应用监控** \> **应用列表**，并在顶部菜单栏选择目标地域。

3.  在应用列表页面右上角单击**接入应用**。

4.  在**接入应用**页面顶部复制License Key。

    ![应用监控LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6570348951/p132858.png)


## 步骤二：集成已有镜像

编辑Dockerfile文件来集成\{original-docker-image:tag\}镜像，您可以参考以下Dockerfile示例文件。

```
###################################
##                              ###
##      ARMS APM DEMO Docker    ###
##          For Java            ###
##      withAgent   V0.1        ###
##                              ###
###################################
# 将{original-docker-image:tag}替换为您的镜像地址。
FROM {original-docker-image:tag}
WORKDIR /root/
# 根据所在地域替换Agent的下载地址。
RUN wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
RUN unzip ArmsAgent.zip -d /root/
# 按照步骤一的说明获取License Key。
# {AppName}为自定义ARMS监控应用名称，不可包含中文字符。
# 若所有镜像都接入同一个应用监控任务，配置此处的arms_licenseKey和arms_appName即可。
# 若需将镜像接入其他应用监控任务，可在docker run命令中使用-e参数指定该应用的arms_licenseKey和arms_appName参数，以覆盖此处的配置。
ENV arms_licenseKey={LicenseKey}
ENV arms_appName={AppName}
ENV JAVA_TOOL_OPTIONS ${JAVA_TOOL_OPTIONS} '-javaagent:/root/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey='${arms_licenseKey}' -Darms.appName='${arms_appName}
### for check the args
RUN env | grep JAVA_TOOL_OPTIONS
### 可在下方添加自定义Dockerfile逻辑。
### ......
```

请按照以下说明替换上述配置文件中的示例值。

-   将`{original-docker-image:tag}`替换为您的镜像地址。若您没有自定义镜像，可使用系统镜像。
-   根据所在地域替换Agent的下载地址。

    **说明：** 请使用公网地址，如无法下载则使用VPC地址。

    |地域|公网地址|VPC地址|
    |--|----|-----|
    |华东1（杭州）|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华东2（上海）|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-shanghai.oss-cn-shanghai-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华北1（青岛）|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-qingdao.oss-cn-qingdao-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华北2（北京）|    ```
wget "http://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-beijing.oss-cn-beijing-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华北3（张家口）|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-zhangjiakou.oss-cn-zhangjiakou-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华南1（深圳）|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-shenzhen.oss-cn-shenzhen-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |中国（香港）|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-hongkong.oss-cn-hongkong-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |亚太东南（新加坡）|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-ap-southeast.oss-ap-southeast-1-internal.aliyuncs.com/cloud_ap-southeast-1/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |日本（东京）|    ```
wget "http://arms-apm-japan.oss-ap-northeast-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-japan.oss-ap-northeast-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |美西（硅谷）|    ```
wget "http://arms-apm-usw.oss-us-west-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-usw.oss-us-west-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华东1金融云|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-hangzhou.oss-cn-hangzhou-internal.aliyuncs.com/finance/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华东2金融云|    ```
wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "http://arms-apm-sh-finance-1.oss-cn-shanghai-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |
    |华南1金融云|    ```
wget "http://arms-apm-sz-finance.oss-cn-shenzhen-finance-1.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ```

|    ```
wget "https://arms-apm-sz-finance.oss-cn-shenzhen-finance-1-internal.aliyuncs.com/ArmsAgent.zip" -O ArmsAgent.zip
    ``` |

-   将`{LicenseKey}`替换成您的License Key。将`{AppName}`替换成您的应用名称（应用名不可包含中文字符）。

## 步骤三：构建并启动新镜像

1.  运行`docker build`命令来构建镜像。

    ```
    docker build -t registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1 -f /{workspace}/Dockerfile /{workspace}/
    ```

    **说明：** 将`registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1`替换为真实镜像名称。

2.  运行`docker run`命令来启动镜像。若需将镜像接入其他应用监控任务，可在`docker run`命令中使用-e参数指定该应用的arms\_licenseKey和arms\_appName参数，以覆盖Dockerfile中的配置。

    ```
    docker run -d -e "arms_licenseKey={LicenseKey}" -e "arms_appName={AppName}" -p 8081:8080 registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1
    ```

    **说明：** 将`{LicenseKey}`替换成您的License Key。将`{AppName}`替换成您的应用名称（应用名不可包含中文字符）。将`registry.cn-hangzhou.aliyuncs.com/arms-docker-repo/arms-springboot-demo:v0.1`替换为真实镜像名称。


## 结果验证

约一分钟后，若您的应用名称出现在应用列表中且有数据上报，则说明接入成功。

## 卸载Agent

当您不需要再监控Docker集群中的Java应用时，请按照以下步骤卸载Agent。

1.  删除按照[步骤二：集成已有镜像](#section_trt_vzp_n2b)的说明添加的Dockerfile内容。

2.  运行`docker build`命令来构建镜像。

3.  运行`docker run`命令来启动镜像。


## 更多信息

**相关文档**  


[应用监控常见问题](/cn.zh-CN/应用监控/应用监控常见问题.md)

