# 使用阿里云Prometheus监控MySQL

阿里云Prometheus监控提供一键安装配置MySQL类型Exporter的功能，并提供开箱即用的专属监控大盘。

## 功能入口

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击目标K8s集群名称。

4.  在左侧导航栏单击**Exporter接入**。


## 添加MySQL类型的Exporter

1.  在**Exporter接入**页面，单击右上角的**添加Exporter**。

2.  在**Exporter列表**对话框右上角的搜索框中，输入要添加的Exporter名称，并在筛选结果中单击目标Exporter图标。

3.  在MySql Exporter配置对话框的**配置**页签输入各项参数。

    ![MySql Exporter配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1621524161/p243566.png)

    |参数|描述|
    |--|--|
    |**Exporter名称**|Exporter的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
默认名称由Exporter类型及数字后缀组成。|
    |**MySql地址**|MySQL的连接地址。**说明：** 支持部署在容器服务Kubernetes版、云服务器ECS、云数据库RDS的MySQL地址联想。 |
    |**MySql端口**|MySQL的端口号，例如：3306。|
    |**用户名**|MySQL的用户名称。|
    |**密码**|MySQL的密码。|

4.  在MySql Exporter配置对话框的**指标**页签查看监控指标。

5.  在MySql Exporter配置对话框的**高级配置**页签设置Exporter采集数据时可以使用的最大CPU核数和内存。

6.  配置完成后，单击**确定**。

7.  在**Exporter接入**页面，单击**大盘**列的大盘链接，查看Prometheus监控大盘。

    ![pg_prom_dashboard_mysql](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6184298951/p97619.png)

8.  在**Exporter接入**页面，可对已添加的Exporter执行以下操作：

    -   单击**操作**列的**删除**，可删除已添加的Exporter。
    -   单击**操作**列的**日志**，可查看Exporter的运行日志。
    -   单击**操作**列的**详情**，可查看Exporter的详情，包括Exporter的环境变量和描述信息。

**相关文档**  


[其他类型的Exporter接入]()

