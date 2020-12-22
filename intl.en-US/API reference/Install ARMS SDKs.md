# Install ARMS SDKs

Application Real-Time Monitoring Service \(ARMS\) provides SDKs for Java, Python, and PHP. This topic describes how to install the SDKs.

## Install ARMS SDK for Java

Add the following Maven dependency to the pom.xml file to install ARMS SDK for Java:

```
<dependencies>
    <dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-arms</artifactId>
       <version>2.7.9</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.7</version>
    </dependency>
</dependencies>
```

## Install ARMS SDK for Python

Run the following command to install SDK for Python:

```
pip install aliyun-python-sdk-arms
```

## Install ARMS SDK for PHP

Perform the following steps to install ARMS SDK for PHP.

1.  Run the following command to clone the PHP SDK to your local folder aliyun-openapi-php-sdk:

    ```
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk
    ```

2.  Copy the aliyun-php-sdk-arms and aliyun-php-sdk-core folders from the aliyun-openapi-php-sdk folder to your PHP project directory. The following figure shoes the directory tree.

    ![PHP Directory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/152342/156509060743309_en-US.png)


**Related topics**  


[List of API operations by feature](/intl.en-US/API reference/API overview.md)

