# Use ARMS Prometheus Monitoring to access and monitor cloud services

Prometheus Monitoring is integrated with Cloud Monitor. You can use Prometheus Monitoring in conjunction with Cloud Monitor to monitor cloud services in the current Alibaba Cloud account within a specific region. This topic describes how to connect cloud services to Prometheus Monitoring and use Grafana dashboards to monitor data of the cloud services.

Cloud Monitor is a service that monitors Alibaba Cloud resources and Internet applications. For more information, see [Cloud Monitor](https://www.aliyun.com/product/jiankong).

After Prometheus Monitoring is integrated with Cloud Monitor, no additional fees are charged for using Cloud Monitor. You are charged based on the billing rules of Prometheus Monitoring. For more information about the billing rules of Prometheus Monitoring, see [Commercial release announcement regarding ARMS Prometheus Monitoring]().

## Procedure

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner of the Prometheus Monitoring page, select a region and click the name of the ACK cluster that you want to view.

3.  In the left-side navigation pane, click **Cloud Services**.


## Access cloud services

1.  In the upper-right corner of the **Cloud service collection list** page, click **Add Cloud Services**.

2.  In the **Add Cloud Services** dialog box, select the services to be monitored and click **OK**.

    You can select one or more of the following cloud services: ECS, ApsaraDB for MongoDB, ApsaraDB for Redis, OSS, ApsaraDB RDS for MySQL, NAT Gateway, SLB, Message Queue for Apache RocketMQ, Message Queue for Apache Kafka, EIP, Elasticsearch, and PolarDB-X.

    ![Add Cloud Services](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6982672161/p184987.png)

    After you select the cloud services, go back to the **Cloud service collection list** page. Information of the selected services is displayed.

    ![Cloud service collection list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6982672161/p184990.png)

    If you need to adjust the selected cloud services, click **Edit** in the **Actions** column. In the **Add Cloud Services** dialog box, re-select cloud services and click **OK**.


## Monitor cloud services

After the cloud services are connected to Prometheus Monitoring, you can monitor the summary data of all selected services and detailed data of each service by using Grafana dashboards.

1.  On the **Cloud service collection list** page, click the dashboard link of the cloud service that you want to monitor in the **Type** column.

    Dashboard links of all selected cloud services and their summary data are displayed in the **Type** column.

2.  On the Grafana dashboard page, view the monitoring data of the selected cloud services.

    ![Cloud service monitoring-Grafana dashboard-overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6629468061/p185064.png)


