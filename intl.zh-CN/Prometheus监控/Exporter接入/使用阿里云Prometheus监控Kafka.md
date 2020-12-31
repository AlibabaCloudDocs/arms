# 使用阿里云Prometheus监控Kafka

阿里云Prometheus监控提供一键安装配置Kafka类型Exporter的功能，并提供开箱即用的专属监控大盘。

## 功能入口

1.  登录[ARMS控制台](https://arms-ap-southeast-1.console.aliyun.com/#/home)。

2.  在左侧导航栏单击**Prometheus监控**。

3.  在页面左上角选择目标地域，然后单击目标K8s集群名称。

4.  在左侧导航栏单击**Exporter接入**。


## 添加Kafka类型的Exporter

1.  在**Exporter接入**页面，单击右上角的**添加Exporter**。

2.  在**Exporter列表**对话框右上角的搜索框中，输入要添加的Exporter名称，并在筛选结果中单击目标Exporter图标。

3.  在kafka Exporter配置对话框的**配置**页签输入各项参数，并单击**确定**。

    |参数|描述|
    |--|--|
    |**Exporter名称**|Exporter的名称命名规范要求如下：    -   仅可包含小写字母、数字和短划线（-），且短划线不可出现在开头或结尾。
    -   名称具有唯一性。
默认名称由Exporter类型及数字后缀组成。|
    |**kafka地址**|Kafka的连接地址。|
    |**kafka端口**|Kafka的端口号，例如：9092。|

4.  在**Exporter接入**页面，单击**面板**列的大盘链接，查看Prometheus监控大盘。

    ![pg_prom_dashboard_kafka](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2284298951/p97643.png)

5.  在**Exporter接入**页面，可对已添加的Exporter执行以下操作：

    -   单击**操作**列的**删除**，可删除已添加的Exporter。
    -   单击**操作**列的**日志**，可查看Exporter的运行日志。
    -   单击**操作**列的**详情**，可查看Exporter的详情，包括Exporter的环境变量和描述信息。

**相关文档**  


[其他类型的Exporter接入]()

