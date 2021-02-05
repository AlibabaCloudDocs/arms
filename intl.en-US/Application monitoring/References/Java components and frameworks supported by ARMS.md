---
keyword: [arms, application monitoring, java, component, framework, filter]
---

# Java components and frameworks supported by ARMS

This topic describes third-party Java components and frameworks supported by Application Real-Time Monitoring Service \(ARMS\). If the components or frameworks used by the application that you want to monitor are not supported by ARMS, you must configure a universal filter to collect monitoring data.

## Java components and frameworks supported by ARMS

|Component|JDK 1.7|JDK 1.8|
|---------|-------|-------|
|Active MQ|5.13.X+|5.13.X+|
|Aliware MQ|4.1.X+|4.1.X+|
|Druid|Not supported|1.0.X+|
|Daojia Service Framework \(DSF\)|Not supported|2.1.X+|
|Dubbo|2.5.X+|2.5.X+|
|Feign|Not supported|9.X+|
|Google HTTP Client|1.10.X+|1.10.X+|
|GRPC-Java|1.15+|1.15+|
|High Speed Framework \(Ali-HSF\)|2.2.4.6-TLS+|2.2.4.6-TLS+|
|HttpClient 3|3.X+|3.X+|
|HttpClient 4|4.X+|4.X+|
|Hystrix|1.5.X+|1.5.X+|
|JDK HTTP|1.7.X+|1.7.X+|
|Jedis|2.4.X+|2.4.X+|
|Jetty|8.X+|8.X+|
|Lettuce|4.0+|4.0+|
|MariaDB|1.3+|1.3+|
|MemCached|2.8+|2.8+|
|MongoDB|3.7+|3.7+|
|MyBatis|3.X+|3.X+|
|MySQL JDBC|5.0.X+|5.0.X+|
|OKHttp|2.X+|2.X+|
|Oracle JDBC|10.2.X+|10.2.X+|
|Play Framework|Not supported|1.4.X|
|PostgreSql JDBC|9.4+|9.4+|
|Rabbit MQ|Not supported|2.1.X+|
|Reactor|Not supported|3.X+|
|Reactor Netty|Not supported|0.9+|
|Redis|2.X+|2.X+|
|Resin|3.0+|3.0+|
|RxJava|2.X+|2.X+|
|Spring|4.X+|4.X+|
|Spring Boot|1.3.X+|1.3.X+|
|Spring Cloud Gateway|Not supported|5.0.0.RELEASE+|
|Spring WebMVC|Not supported|5.0.6.RELEASE+|
|Spring WebFlux|Not supported|5.0.0.RELEASE+|
|SQLServer JDBC|6.4+|6.4+|
|Thrift|0.8+|0.8+|
|Tomcat|7.X+|7.X+|
|Undertow|1.3X+|1.3X+|
|WebLogic|12.X+|12.X+|

## Configure a universal filter to collect data

If the components or frameworks of an application are not supported by ARMS, you must configure a universal filter to collect data. Perform the following operations:

1.  Import arms-sdk-1.7.1.jar to the pom.xml file.

    ```
    <dependency>
        <groupId>com.alibaba.arms.apm</groupId>
        <artifactId>arms-sdk</artifactId>
        <version>1.7.1</version>
    </dependency>
    ```

    **Note:** If you cannot obtain pom.xml, download [arms-sdk-1.7.1.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.1.jar).

2.  Configure the filter of ARMS in web.xml.

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

3.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
4.  Install the ARMS agent for the Java application. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Quick start/Monitor Java applications/Manually install the ARMS agent for a Java application.md).
5.  Restart the application for the configuration to take effect.

