# ARMS Agent安装成功，为什么控制台上仍无监控数据？

## Condition

ARMS Agent安装成功，控制台上仍无监控数据。

## Cause

应用无持续的外部请求访问、应用所属地域和ARMS Agent所属地域不一致、或者ARMS Agent安装目录权限不正确等原因都有可能导致控制台无监控数据。

1.  如果Agent日志中出现“send agent metrics. no metrics.”，请确认您的应用是否有持续的外部请求访问，包括HTTP请求、HSF请求和Dubbo请求，并确认开发框架是否在ArmsAgent的支持范围内。关于ARMS应用监控对第三方组件和框架的支持情况，请参见[ARMS 应用监控支持的 Java 组件和框架](/cn.zh-CN/应用监控/参考信息/ARMS 应用监控支持的 Java 组件和框架.md)和[ARMS 应用监控支持的 PHP 组件和框架](/cn.zh-CN/应用监控/参考信息/ARMS 应用监控支持的 PHP 组件和框架.md)。

2.  确认选择的查询时间范围是否正确。请您将查询时间条件设为最近15分钟，然后再次确认是否有监控数据。

3.  如果是通过`-jar`命令行启动的，请检查命令行设置，确保-javaagent参数在`-jar`之前。

    ```
    java -javaagent:/{user.workspace}/ArmsAgent/arms-bootstrap-1.7.0-SNAPSHOT.jar -Darms.licenseKey=xxx -Darms.appName=xxx -jar demoApp.jar
    ```

4.  如果ArmsAgent/log/ 下的日志中出现LicenseKey is invalid.异常，请您检查应用所属地域与Agent所属地域是否一致。

5.  如果应用启动之后ArmsAgent目录下无log子目录，是由于arms-bootstrap-1.7.0-SNAPSHOT.jar未被成功加载导致的，请您检查ArmsAgent安装目录的权限是否正确。

6.  若应用启动时出现以下报错，请您检查arms-bootstrap-1.7.0-SNAPSHOT.jar软件包及相应权限是否正确。

    ![Application Start Error](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3970348951/p43213.png)

7.  如果仍无监控数据，请打包Java探针日志（路径：ArmsAgent/log），并联系钉钉服务账号`arms160804`解决问题。

8.  检查JDK版本。

    -   如果JDK版本为1.8.0\_25或者1.8.0\_31，可能会出现无法安装探针的情况，建议您升级对应的JDK版本，或咨询钉钉服务账号`arms160804`。
    -   如果JDK版本为1.10.X，需通过以下地址下载对应的Agent安装包。
        -   [华东1（杭州）](https://arms-apm-hangzhou.oss-cn-hangzhou.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [华东2（上海）](https://arms-apm-shanghai.oss-cn-shanghai.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [华北1（青岛）](https://arms-apm-qingdao.oss-cn-qingdao.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [华北2（北京）](https://arms-apm-beijing.oss-cn-beijing.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [华北3（张家口）](https://arms-apm-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [华南1（深圳）](https://arms-apm-shenzhen.oss-cn-shenzhen.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)
        -   [中国香港](https://arms-apm-hongkong.oss-cn-hongkong.aliyuncs.com/2.7.2/ArmsAgent.tar.gz)

