# Use Prometheus Service to monitor NGINX exporters \(earlier version\)

Alibaba Cloud Prometheus Service allows you to install and configure NGINX exporters, and provides out-of-the-box dashboards. This topic describes how to install and configure NGINX exporters of the earlier version.

-   The nginx-module-vts module is installed for the NGINX exporters of the earlier version.
-   The following table lists the metrics of NGINX exporters of the earlier version.

    |Metric|Type|Description|
    |------|----|-----------|
    |nginx\_server\_requests|Server|The number of server requests.|
    |nginx\_server\_bytes|Server|The number of bytes processed by the server.|
    |nginx\_server\_cache|Server|The cache of the server.|
    |nginx\_filter\_requests|Filter|The number of filter requests.|
    |nginx\_filter\_bytes|Filter|The number of bytes processed by the filter.|
    |nginx\_\_filter\_responseMsec|Filter|The response time of the filter.|
    |nginx\_upstream\_requests|Upstreams|The number of upstream requests.|
    |nginx\_upstream\_bytes|Upstreams|The number of upstream bytes.|
    |nginx\_upstream\_responseMsec|Upstreams|The upstream response time.|


## Entry

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner, select the target region and click the name of the target Kubernetes cluster.

4.  In the left-side navigation pane, click **Exporter access**.


## Add an NGINX exporter

1.  On the **Exporter access** page, click **add Exporter** in the upper-right corner.

2.  In the search box in the upper-right corner of the **Exporter list** dialog box, enter an Exporter name and click the target Exporter icon.

3.  In the Nginx Exporter configuration dialog box, set the required parameters on the **Configuration** tab, and then click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |**Exporter name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**NginxAddress**|The URL that is used to access the NGINX server.|
    |**NginxPort**|The port number of the NGINX server, for example, 80.|

    **Note:** You must first install nginx-module-vts. This NGINX virtual host traffic status module can output data in the JSON format.

4.  On the **Exporters** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_Nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7307468061/p97649.png)

5.  On the **Exporters** page, you can perform the following operations on the added Exporter:

    -   Click **Delete** in the **Actions** column to delete the Exporter.
    -   Click **Log** in the **Actions** column to view the operational logs of the Exporter.
    -   Click **Details** in the **Actions** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Prometheus Monitoring to monitor NGINX exporters \(later version\)]()

[Use Prometheus Service to monitor other exporters]()

