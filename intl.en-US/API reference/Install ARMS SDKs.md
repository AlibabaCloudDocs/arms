# Install ARMS SDKs

Application Real-Time Monitoring Service \(ARMS\) provides SDKs for Java, Python, and PHP applications. This topic explains how to install the SDKs.

## Install the Java SDK

To install the ARMS Java SDK, add the Maven dependency to the pom.xml file.

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

## Install the Python SDK

To install the ARMS Python SDK, run the following command:

```
pip install aliyun-python-sdk-arms
```

## Install the PHP SDK

Follow these steps to install the ARMS PHP SDK.

1.  Run the following command to clone the PHP SDK to your local directory aliyun-openapi-php-sdk:

    ```
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk
    ```

2.  Copy folders aliyun-php-sdk-arms and aliyun-php-sdk-core under aliyun-openapi-php-sdk to your PHP project directory. The directory structure is as follows:

    ![PHP Directory](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/152342/156509060743309_en-US.png)


