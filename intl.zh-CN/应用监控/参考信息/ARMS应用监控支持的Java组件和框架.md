---
keyword: [ARMS, 应用监控, Java, 组件, 框架, Filter]
---

# ARMS应用监控支持的Java组件和框架

本文列出了ARMS应用监控支持的Java第三方组件和框架。如果待监控应用使用的组件或框架不在支持范围内，则需要通过配置通用Filter拦截器的方式进行监控数据采集。

## ARMS应用监控支持的Java组件和框架

|组件|JDK 1.7|JDK 1.8|
|--|-------|-------|
|Dubbo|2.5.X+|2.5.X+|
|Feign|不支持|9.X+|
|Google HTTP Client|1.10.X+|1.10.X+|
|GRPC-Java|1.15+|1.15+|
|HttpClient 3|3.X+|3.X+|
|HttpClient 4|4.X+|4.X+|
|Hystrix|1.5.X+|1.5.X+|
|JDK HTTP|1.7.X+|1.7.X+|
|Jetty|8.X+|8.X+|
|Lettuce|4.0+|4.0+|
|MariaDB|1.3+|1.3+|
|MemCached|2.8+|2.8+|
|MongoDB|3.7+|3.7+|
|MyBatis|3.X+|3.X+|
|MySQL JDBC|5.0.X+|5.0.X+|
|OKHttp|2.X+|2.X+|
|Oracle JDBC|10.2.X+|10.2.X+|
|PostgreSql JDBC|9.4+|9.4+|
|Reactor|不支持|3.X+|
|Reactor Netty|不支持|0.9+|
|Redis|2.X+|2.X+|
|Resin|3.0+|3.0+|
|RxJava|2.X+|2.X+|
|Spring|4.X+|4.X+|
|Spring Boot|1.3.X+|1.3.X+|
|Spring Cloud Gateway|不支持|5.0.0.RELEASE+|
|Spring WebFlux|不支持|5.0.0.RELEASE+5.0.0.RELEASE+|
|SQLServer JDBC|6.4+|6.4+|
|Thrift|0.8+|0.8+|
|Tomcat|7.X+|7.X+|
|Undertow|1.3X+|1.3X+|
|WebLogic|12.X+|12.X+|

## 配置通用Filter拦截器以采集数据

如果应用的组件或框架不在支持范围内，可以通过配置通用Filter拦截器的方式采集数据。配置步骤：

1.  在工程的POM文件中引入arms-sdk-1.7.1.jar。

    ```
    <dependency>
        <groupId>com.alibaba.arms.apm</groupId>
        <artifactId>arms-sdk</artifactId>
        <version>1.7.1</version>
    </dependency>
    ```

    **说明：** 如果无法获取POM文件，请下载[arms-sdk-1.7.1.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.1.jar)。

2.  在web.xml中配置ARMS的Filter拦截器。

    ```
    <filter>
        <filter-name>EagleEyeFilter</filter-name>
        <filter-class>com.alibaba.arms.filter.EagleEyeFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>EagleEyeFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

3.  登录[ARMS控制台](https://arms-intl.console.aliyun.com/)。
4.  [为Java应用安装探针](/intl.zh-CN/应用监控/开始监控 Java 应用/为Java应用手动安装Agent.md)。
5.  重启应用令配置生效。

