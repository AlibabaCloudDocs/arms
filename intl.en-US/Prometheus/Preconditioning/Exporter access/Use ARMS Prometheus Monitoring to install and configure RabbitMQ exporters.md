# Use ARMS Prometheus Monitoring to install and configure RabbitMQ exporters

Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring enables you to install and configure RabbitMQ exporters, and provides out-of-the-box dashboards.

## Entry

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner, select the target region and click the name of the target Kubernetes cluster.

4.  In the left-side navigation pane, click **Exporter access**.


## Add a RabbitMQ exporter

1.  On the **Exporter access** page, click **add Exporter** in the upper-right corner.

2.  In the search box in the upper-right corner of the **Exporter list** dialog box, enter an Exporter name and click the target Exporter icon.

3.  In the RabbitMQ Exporter Configuration dialog box, set parameters and click **OK**.

    ![db_prom_exporter_rabbitmq](../images/p97644.png)

    |Parameter|Description|
    |---------|-----------|
    |**Exporter Name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**RabbitMQ Address**|The connection URL of the RabbitMQ system.|
    |**RabbitMQ Port**|The port number of the RabbitMQ system, for example, 15672.|
    |**Username**|The user name for connecting to the RabbitMQ system.|
    |**Password**|The password for connecting to the RabbitMQ system.|

4.  On the **Exporter** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_rabbitmq](../images/p97645.png)

5.  On the **Exporter access** page, you can perform the following operations on the added Exporter:

    -   Click **operation** in the **delete** column to delete the Exporter.
    -   Click **operation** in the **log** column to view the operational logs of the Exporter.
    -   Click **operation** in the **details** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Prometheus Service to monitor other exporters]()

