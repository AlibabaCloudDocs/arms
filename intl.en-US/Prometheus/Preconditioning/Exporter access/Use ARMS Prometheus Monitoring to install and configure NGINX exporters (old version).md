# Use ARMS Prometheus Monitoring to install and configure NGINX exporters \(old version\)

Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring enables you to install and configure NGINX exporters, and provides out-of-the-box dashboards. This topic describes how to install and configure NGINX exporters of the old version.

-   The nginx-module-vts module is installed for the NGINX exporters of the old version.
-   The following table lists metrics of NGINX exporters of the old version.

    |Metric|Type|Description|
    |------|----|-----------|
    |nginx\_server\_requests|Server|The number of server requests.|
    |nginx\_server\_bytes|Server|The number of server bytes.|
    |nginx\_server\_cache|Server|The server cache.|
    |nginx\_filter\_requests|Filter|The number of filter requests.|
    |nginx\_filter\_bytes|Filter|The number of filter bytes.|
    |nginx\_\_filter\_responseMsec|Filter|The filter response time.|
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

3.  In the NGINX Exporter Configuration dialog box, set parameters and click **OK**.

    ![db_prom_exporter_Nginx](../images/p97646.png)

    |Parameter|Description|
    |---------|-----------|
    |**Exporter Name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**NGINX Address**|The connection URL of the NGINX server.|
    |**NGINX Port**|The port number of the NGINX server, for example, 80.|

    **Note:** You must install nginx-module-vts first. This NGINX virtual host traffic status module can output data in JSON format.

4.  On the **Exporter** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_Nginx](../images/p97649.png)

5.  On the **Exporter access** page, you can perform the following operations on the added Exporter:

    -   Click **operation** in the **delete** column to delete the Exporter.
    -   Click **operation** in the **log** column to view the operational logs of the Exporter.
    -   Click **operation** in the **details** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Alibaba Cloud Prometheus to monitor Nginx \(new version\)]()

[Use Prometheus Service to monitor other exporters]()

