# 安装 ARMS SDK {#task_51904_zh .task}

ARMS 提供 Java、Python 和 PHP 的 SDK，本文介绍安装方法。

## 安装 Java SDK {#section_50g_918_z8l .section}

要安装 ARMS Java SDK，只需在 pom.xml 文件中添加 Maven 依赖即可。

``` {#codeblock_l3h_ptm_20j}
<dependencies>
    <dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-arms</artifactId>
       <version>2.5.2</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>3.5.0</version>
    </dependency>
</dependencies>
```

## 安装 Python SDK {#section_ldi_46m_oym .section}

要安装 ARMS Python SDK，请运行以下命令：

``` {#codeblock_bpv_sqm_de3}
pip install aliyun-python-sdk-arms
```

## 安装 PHP SDK {#section_r7c_k4e_mz7 .section}

请按照以下步骤安装 PHP SDK。

1.  运行以下命令，将 PHP SDK 克隆到本地的 aliyun-openapi-php-sdk 文件夹。 

    ``` {#codeblock_w3f_g33_1q6}
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk
    ```

2.  将 aliyun-openapi-php-sdk 下的 aliyun-php-sdk-arms 和 aliyun-php-sdk-core 文件夹复制到您的 PHP 项目目录，目录结构如下图所示。 ![PHP Directory](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152342/156647424143309_zh-CN.png) 

