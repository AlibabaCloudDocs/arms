# Use Prometheus Monitoring to monitor NGINX exporters \(later version\)

Alibaba Cloud Prometheus Monitoring allows you to install and configure NGINX exporters, and provides out-of-the-box dashboards. This topic describes how to install and configure NGINX exporters of the new version.

You have installed and run the NGINX service.

-   The NGINX status monitoring module ngx\_http\_stub\_status\_module collects statistics for the number of requests received and handled by the NGINX service.
-   The ngx\_http\_stub\_status\_module module is installed for the NGINX exporters of the later version.
-   The following table lists the metrics of NGINX exporters of the later version.

    |Metric|Description|
    |------|-----------|
    |nginx\_connections\_accepted|The number of accepted client connections.|
    |nginx\_connections\_active|The number of current client connections.|
    |nginx\_connections\_handled|The number of handled client connections.|
    |nginx\_connections\_reading|The number of read client connections.|
    |nginx\_connections\_waiting|The number of waiting client connections.|
    |nginx\_connections\_writing|The number of write-back client connections.|
    |nginx\_http\_requests\_total|The total number of client requests.|
    |nginx\_up|Specifies whether an NGINX exporter runs properly|
    |nginxexporter\_build\_info|The build information of the NGINX exporter.|


## Step 1: Install the ngx\_http\_stub\_status\_module module

If the NGINX service is running on an Elastic Compute Service \(ECS\) instance, perform the following steps to install an NGINX exporter:

1.  Check whether the ngx\_http\_stub\_status\_module module is installed.

    ```
    nginx -V 2>&1 | grep -o with-http_stub_status_module
    ```

    -   A similar output indicates that the ngx\_http\_stub\_status\_module module is installed.

        ![cw_prom_exporter_nginx_module](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6027468061/p128838.png)

    -   If the preceding information does not appear, the ngx\_http\_stub\_status\_module module is not installed. Run the following commands to install the module:

        ```
        wget http://nginx.org/download/nginx-1.13.12.tar.gz
        tar xfz nginx-1.13.12.tar.gz
        cd nginx-1.13.12/
        ./configure --with-http_stub_status_module
        make
        make install
        ```

2.  Start the ngx\_http\_stub\_status\_module module to query the NGINX status.

    ```
    location /nginx_status {
      stub_status on;
      allow 127.0.0.1;  #only allow requests from localhost
      deny all;   #deny all other hosts 
     }
    ```

    **Note:**

    -   The value of location must be `nginx_status`.
    -   `allow 127.0.0.1` and `deny all` allow only local access. To allow NGINX exporter access, comment out these two lines of code, or change `127.0.0.1` to the IP address of the NGINX exporter.
3.  Restart NGINX.

    ```
    nginx -t
    nginx -s reload 
    ```

4.  Check whether the ngx\_http\_stub\_status\_module module is started.

    ```
    curl http://127.0.0.1/nginx_status
    ```

    A similar output indicates that the ngx\_http\_stub\_status\_module module is started.

    ![cw_prom_exporter_nginx_module_success](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6027468061/p128860.png)


## Step 2: Install an NGINX exporter of the later version

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the upper-left corner, select the target region and click the name of the target Kubernetes cluster.

3.  In the left-side navigation pane, click **Exporter access**.

4.  On the **Exporter access** page, click **add Exporter** in the upper-right corner.

5.  In the search box in the upper-right corner of the **Exporter list** dialog box, enter an Exporter name and click the target Exporter icon.

6.  In the Nginx\(V2\) Exporter configuration dialog box, configure the required parameters on the **Configuration** tab. Click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |**Exporter name**|The name of the exporter. The name must meet the following requirements:    -   It can contain only lowercase letters, digits, and hyphens \(-\), and cannot start or end with a hyphen \(-\).
    -   It must be unique.
If you do not specify this parameter, the system uses the default name that consists of the exporter type and a numeric suffix.|
    |**Nginx\(v2\) Address**|The URL that is used to access the NGINX server.|
    |**Nginx\(v2\) Port**|The port number of the NGINX server. Example: 80.|

7.  On the **Exporters** page, click the DASHBOARD link in the **dashboard** column to view the Prometheus dashboard.

    ![pg_prom_dashboard_Nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7307468061/p97649.png)

8.  On the **Exporters** page, you can perform the following operations on the added Exporter:

    -   Click **Delete** in the **Actions** column to delete the Exporter.
    -   Click **Log** in the **Actions** column to view the operational logs of the Exporter.
    -   Click **Details** in the **Actions** column to view the Exporter details, including the environment variables and description of the Exporter.

**Related topics**  


[Use Prometheus Service to monitor NGINX exporters \(earlier version\)]()

[Use Prometheus Service to monitor other exporters]()

