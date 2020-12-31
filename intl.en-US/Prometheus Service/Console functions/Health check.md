# Health check

The health check function allows you to check whether the Application Real-Time Monitoring Service \(ARMS\) Prometheus agent is installed. If ARMS Prometheus Monitoring fails to monitor data, you can troubleshoot the problem based on the health check results.

You have completed the procedure of using ARMS Prometheus Monitoring to monitor your applications or components. For more information, see [Overview]().

## Portal

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Prometheus Monitoring**.

3.  On the Prometheus monitoring page, click the Kubernetes cluster to be viewed.

4.  In the left-side navigation pane, choose **Health Check**.


## View health check results

On the Health Check page, view the health check results. The health check results contain the runtime data of ARMS Prometheus Monitoring sorted by phase, including:

1.  Whether the Grafana dashboard is created properly
2.  Whether the API request is normal

    **Note:** The custom Grafana dashboard and on-premises clusters except for the Kubernetes cluster use API URLs to acquire the data source.

3.  Whether the data collection is successful
4.  Whether Promethues Monitoring metrics are acquired

## Remove metrics

If you want to solve the problem of single-metric explosion or exclude certain metrics from monitoring, you can remove them.

1.  On the Health Check page, click **Remove Metrics** in the upper-right corner.

2.  In the Remove Metrics dialog box, set metricName to the names of metrics to be abandoned. Separate multiple metric names with line breaks.


**Related topics**  


[Overview]()

