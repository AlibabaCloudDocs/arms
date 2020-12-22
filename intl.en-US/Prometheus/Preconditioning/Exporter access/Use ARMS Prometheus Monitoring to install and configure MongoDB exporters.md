# Use ARMS Prometheus Monitoring to install and configure MongoDB exporters

Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring enables you to install and configure MongoDB exporters, and provides out-of-the-box dashboards.

## Entry

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner, select the target region and click the name of the target Kubernetes cluster.

4.  In the left-side navigation pane, click **Exporter access**.


## Add a MongoDB exporter

1.  On the **Exporter access** page, click **add Exporter** in the upper-right corner.

2.  In the search box in the upper-right corner of the **Exporter list** dialog box, enter an Exporter name and click the target Exporter icon.

3.  In the MongoDB Exporter Configuration dialog box, set parameters and click **OK**.

    ![db_prom_exporter_mongodb](../images/p97638.png)

    |Parameter|Description|
    |---------|-----------|
    |**Exporter Name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**MongoDB Address**|The connection URL of the MongoDB database.|
    |**MongoDB Port**|The port number of the MongoDB database, for example, 3717.|
    |**Username**|The user name for connecting to the MongoDB database.|
    |**Password**|The password for connecting to the MongoDB database.|

4.  On the **Exporter** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_mongodb](../images/p97639.png)

5.  On the **Exporter access** page, you can perform the following operations on the added Exporter:

    -   Click **operation** in the **delete** column to delete the Exporter.
    -   Click **operation** in the **log** column to view the operational logs of the Exporter.
    -   Click **operation** in the **details** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Prometheus Service to monitor other exporters]()

