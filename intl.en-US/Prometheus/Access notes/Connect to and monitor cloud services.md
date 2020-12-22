# Connect to and monitor cloud services

Prometheus is integrated with Alibaba Cloud CloudMonitor. You can use CloudMonitor to monitor the cloud services of the current cloud account in the specified region in Prometheus. This topic describes how to connect cloud services to Prometheus and use Grafana to monitor the cloud service data.

Cloud Monitor is a service that monitors Alibaba Cloud resources and Internet applications. For more information, see [CloudMonitor](https://www.aliyun.com/product/jiankong).

After Prometheus is integrated with CloudMonitor, no additional fees are charged for CloudMonitor. The collected monitoring data is charged according to the rules in Prometheus. For more information about the billing rules for Prometheus, see [Commercial release announcement regarding ARMS Prometheus Monitoring](/intl.en-US/Pricing/Commercial release announcement regarding ARMS Prometheus Monitoring.md).

## Procedure

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner of the Prometheus monitoring page, select the target region and click the name of the Kubernetes cluster to be viewed.

3.  In the left-side navigation pane, click **cloud service access**.


## Access cloud services

1.  On the **cloud service collection list** page, click **add cloud service** in the upper-right corner.

2.  In the **add cloud service** dialog box, select the cloud service to be connected, and then click **OK**.

    Currently, Prometheus supports integration with ECS, RDS, MongoDB, Redis, OSS, RDS, NAT, SLB, RocketMQ, Kafka, EIP, ES, and DRDS.

    After the cloud service is accessed, return to the **cloud service collection list** page to view information about the accessed cloud service.

    To modify a cloud service, click **actions** in the **edit** column. In the **add cloud service** dialog box that appears, reselect a cloud service and click **OK**.


## Monitor cloud service data

After the cloud service is connected to Prometheus, you can use the Grafana monitoring dashboard to monitor summary data of cloud services and detailed data of specific cloud services.

1.  In the **cloud service collection list** page, click the link of the cloud service to be monitored in the **type** column.

    The **type** column contains all the cloud service types and the cloud service Overview link.

2.  On the Grafana dashboard page, view the monitoring data of the target service.

    ![Cloud service monitoring-Grafana-Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6629468061/p185064.png)


