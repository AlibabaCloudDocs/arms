# Health check

The health check feature allows you to check whether Alibaba Cloud Prometheus Monitoring is installed. If Prometheus Monitoring fails to monitor data, you can troubleshoot the problem based on the health check results.

The procedure of using Prometheus Monitoring to monitor your applications or components is complete. For more information, see [Overview]().

## Procedure

1.  Log on to the [ARMS console](https://arms.console.aliyun.com/#/home)[ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the upper-left corner of the Prometheus Monitoring page, select a region and click the name of the Kubernetes cluster that you want to view.

4.  In the left-side navigation pane, click **Health Check**.


## View health check results

On the Health Check page, view the health check results. The health check results contain the runtime data of Prometheus Monitoring sorted by phase, including:

1.  Creation of Grafana.
2.  API requests.

    **Note:** The custom Grafana dashboard and user-created clusters except for the Kubernetes cluster use API URLs to obtain data sources.

3.  Collection of statuses when the Kubernetes cluster of Container Service runs.
4.  The number of entries collected by the Prometheus agent and details of each job.
5.  The details of jobs that correspond to metrics to collect data. You can view which jobs are free of charge or paid.
6.  Statistics for the number of metrics.
7.  The number of types of Promethues metrics and the sorting results in the last minute.

## Remove metrics

If you want to solve the problem of too much metric data collected by the agent or exclude specific metrics from monitoring, you can remove these metrics.

1.  On the Health Check page, click **Remove Metrics** in the upper-right corner.

2.  In the Remove Metrics dialog box, set metricName to the names of metrics to be abandoned. Separate multiple metric names with line feeds.


**Related topics**  


[Overview]()

