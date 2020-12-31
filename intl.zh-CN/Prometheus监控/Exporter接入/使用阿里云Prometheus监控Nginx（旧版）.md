# 使用阿里云Prometheus监控Nginx（旧版）

阿里云Prometheus监控提供一键安装配置Nginx类型Exporter的功能，并提供开箱即用的专属监控大盘。本文介绍旧版Nginx类型Exporter的安装配置详情。

-   旧版Nginx类型Exporter安装的是nginx-module-vts模块。
-   旧版Nginx类型Exporter采集的Nginx指标如下表所示。

    |指标|类型|描述|
    |--|--|--|
    |nginx\_server\_requests|Server|Server请求数|
    |nginx\_server\_bytes|Server|Server字节数|
    |nginx\_server\_cache|Server|Server缓存|
    |nginx\_filter\_requests|Filter|Filter请求数|
    |nginx\_filter\_bytes|Filter|Filter字节数|
    |nginx\_\_filter\_responseMsec|Filter|Filter响应时间|
    |nginx\_upstream\_requests|Upstreams|上行请求数|
    |nginx\_upstream\_bytes|Upstreams|上行字节数|
    |nginx\_upstream\_responseMsec|Upstreams|上行响应时间|


## 功能入口

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击目标K8s集群名称。

4.  在左侧导航栏单击**Exporter接入**。


## 添加Nginx类型的Exporter

1.  在**Exporter接入**页面，单击右上角的**添加Exporter**。

2.  在**Exporter列表**对话框右上角的搜索框中，输入要添加的Exporter名称，并在筛选结果中单击目标Exporter图标。

3.  在Nginx Exporter配置对话框的**配置**页签输入各项参数，并单击**确定**。

    |参数|描述|
    |--|--|
    |**Exporter名称**|Exporter的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
默认名称由Exporter类型及数字后缀组成。|
    |**Nginx地址**|Nginx的连接地址。|
    |**Nginx端口**|Nginx的端口号，例如：80。|

    **说明：** 您需要先安装Nginx的监控模块nginx-module-vts：Nginx virtual host traffic status module，此模块可以提供JSON格式的数据产出。

4.  在**Exporter接入**页面，单击**面板**列的大盘链接，查看Prometheus监控大盘。

    ![pg_prom_dashboard_Nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7284298951/p97649.png)

5.  在**Exporter接入**页面，可对已添加的Exporter执行以下操作：

    -   单击**操作**列的**删除**，可删除已添加的Exporter。
    -   单击**操作**列的**日志**，可查看Exporter的运行日志。
    -   单击**操作**列的**详情**，可查看Exporter的详情，包括Exporter的环境变量和描述信息。

**相关文档**  


[使用阿里云Prometheus监控Nginx（新版）]()

[其他类型的Exporter接入]()

