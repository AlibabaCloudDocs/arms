# Install ARMS SDK {#task_51904_zh .task}

ARMS provides SDKs for Java, Python, and PHP. This topic explains how to install the SDKs.

## Install Java SDK {#section_50g_918_z8l .section}

To install ARMS Java SDK, add the Maven dependency to the pom.xml file.

``` {#codeblock_l3h_ptm_20j}
<dependencies>
    <dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-arms</artifactId>
       <version>2.2.0</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>3.5.0</version>
    </dependency>
</dependencies>
```

## Install Python SDK {#section_ldi_46m_oym .section}

To install ARMS Python SDK, run the following command:

``` {#codeblock_bpv_sqm_de3}
pip install aliyun-python-sdk-arms
```

## Install PHP SDK {#section_r7c_k4e_mz7 .section}

Follow these steps to install PHP SDK.

1.  Run the following command to clone the PHP SDK to your local directory aliyun-openapi-php-sdk. 

    ``` {#codeblock_w3f_g33_1q6}
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk
    ```

2.  Copy folders aliyun-php-sdk-arms and aliyun-php-sdk-core under aliyun-openapi-php-sdk to your PHP project directory. The directory structure is as follows: ![PHP Directory](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152342/156509060743309_en-US.png) 

