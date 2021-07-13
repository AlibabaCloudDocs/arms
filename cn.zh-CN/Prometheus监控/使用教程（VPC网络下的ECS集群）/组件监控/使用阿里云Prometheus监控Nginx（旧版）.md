# 使用阿里云Prometheus监控Nginx（旧版）

阿里云Prometheus监控提供一键安装配置Nginx类型的组件，并提供开箱即用的专属监控大盘。本文介绍旧版Nginx类型的组件安装配置详情。

-   旧版Nginx类型的组件安装的是nginx-module-vts模块。
-   旧版Nginx类型的组件采集的Nginx指标如下表所示。

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

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击Prometheus示例实例名称。

4.  在左侧导航栏单击**组件监控**。


## 添加Nginx类型的组件

1.  在组件监控页面，单击右上角的**添加组件监控**。

2.  在组件列表对话框右中单击Nginx组件图标。

3.  在Nginx组件配置对话框的**配置**页签输入各项参数。

    ![Nginx组件监控](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7586416261/p293832.png)

    |参数|描述|
    |--|--|
    |**组件名称**|组件的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
**说明：** 默认名称由组件类型及数字后缀组成。 |
    |**Nginx地址**|Nginx的连接地址。|
    |**Nginx端口**|Nginx的端口号，例如：80。|

    **说明：** 您需要先安装Nginx的监控模块nginx-module-vts：Nginx virtual host traffic status module，此模块可以提供JSON格式的数据产出。

4.  在Nginx组件配置对话框的**指标**页签查看监控指标。

5.  配置完成后，单击**确定**。

6.  在组件监控页面，单击**大盘**列的大盘链接，查看Prometheus监控大盘。

    ![pg_prom_dashboard_Nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7284298951/p97649.png)


## 相关操作

在组件监控页面，可对已添加的组件执行以下操作：

-   单击**操作**列的**删除**，可删除已添加的组件。
-   单击**操作**列的**日志**，可查看组件的运行日志。
-   单击**操作**列的**详情**，可查看组件的详情，包括组件的环境变量和描述信息。

