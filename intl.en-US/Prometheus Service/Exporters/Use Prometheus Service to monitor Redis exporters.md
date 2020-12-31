# Use Prometheus Service to monitor Redis exporters

Alibaba Cloud Prometheus Service allows you to install and configure Redis exporters, and provides out-of-the-box dashboards.

## Entry

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner, select the target region and click the name of the target Kubernetes cluster.

4.  In the left-side navigation pane, click **Exporter access**.


## Add a Redis exporter

1.  On the **Exporter access** page, click **add Exporter** in the upper-right corner.

2.  In the search box in the upper-right corner of the **Exporter list** dialog box, enter an Exporter name and click the target Exporter icon.

3.  In the Redis Exporter configuration dialog box, set the required parameters on the **Configuration** tab, and then click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |**Exporter name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**RedisAddress**|The URL that is used to access the Redis database.|
    |**RedisPort**|The port number of the Redis database, for example, 6379.|
    |**Password**|The password that is used to access the Redis database.|

4.  On the **Exporters** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_redis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0226468061/p97571.png)

5.  On the **Exporters** page, you can perform the following operations on the added Exporter:

    -   Click **Delete** in the **Actions** column to delete the Exporter.
    -   Click **Log** in the **Actions** column to view the operational logs of the Exporter.
    -   Click **Details** in the **Actions** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Prometheus Service to monitor other exporters]()

