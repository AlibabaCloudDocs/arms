# 安装ARMS SDK

ARMS提供Java、Python和PHP的SDK，本文介绍安装方法。

## 安装Java SDK

请在pom.xml文件中添加以下Maven依赖来安装Java SDK。

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

## 安装Python SDK

请运行以下命令安装Python SDK。

```
pip install aliyun-python-sdk-arms
```

## 安装PHP SDK

请按照以下步骤安装PHP SDK。

1.  运行以下命令，将PHP SDK克隆到本地的aliyun-openapi-php-sdk文件夹。

    ```
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk
    ```

2.  将aliyun-openapi-php-sdk下的aliyun-php-sdk-arms和aliyun-php-sdk-core文件夹复制到您的PHP项目目录，目录结构如下图所示。

    ![PHP Directory](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3562034061/p43309.png)


**相关文档**  


[API概览](/intl.zh-CN/API 参考/API概览.md)

