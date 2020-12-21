# ARMS Prometheus Monitoring supports monitoring databases through GUI

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) released an updated version on March 20, 2020. The new version allows you to connect Redis, MySQL, Elasticsearch, and MangoDB to ARMS Prometheus Monitoring and then monitor these databases with a few clicks.

**Note:** You can try ARMS Prometheus Monitoring free for 15 days. [Click here to start your free trial](https://common-buy.aliyun.com/?&commodityCode=arms#/open). We welcome you to join the DingTalk group for free trial users: 23155358.

## Overview of ARMS Prometheus Monitoring

ARMS Prometheus Monitoring provides all-in-one and ready-to-use Prometheus monitoring services with the following features:

-   Simplified and stable Prometheus collectors: Prometheus collectors are deployed in your cluster using Helm charts. Based on simplified and optimized Prometheus servers, Prometheus collectors focus on service discovery and data collection. The resource consumption of a Prometheus collector is reduced to 5% of the resource consumption of a Prometheus server. Prometheus collectors support horizontal scaling.
-   Stable and large-capacity cloud storage: Cloud storage is based on Alibaba Cloud Log Service and provides virtually unlimited storage as well as efficient and stable distributed storage.
-   Efficient and powerful capability to query data in the cloud: Prometheus servers in the cloud provide a metric query capability that is fully compatible with PromQL, with the additional features of downsampling and speeding up queries.
-   Default alerting service: ARMS Prometheus Monitoring supports native alerting rules and provides multiple alert notification channels by default, such as email and DingTalk. Alert notifications can be sent to relevant contacts through the cloud monitoring service.
-   Ready-to-use monitoring dashboards for Grafana Cloud: By default, ARMS Prometheus Monitoring provides monitoring dashboards for Kubernetes clusters, allowing you to monitor hosts, pods, deployments, API servers, Ingress, and coreDNS. It also provides monitoring dashboards for various third-party components.

For more information about ARMS Prometheus Monitoring, see [What is Prometheus Service?]().

## One-click database monitoring

ARMS Prometheus Monitoring supports one-click access to monitor mainstream databases. To view your dashboard for database monitoring, follow these steps:

1.  Select the type of the database that you want to monitor.

    Currently, only Redis, MySQL, Elasticsearch, and MangoDB databases are supported.

    ![pg_prom_choose_database](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94349.png)

2.  Set the parameters for the monitored database.

    Take MangoDB as an example. Enter the exporter name, and the connect string, port number, username, and password of the MangoDB database.

    ![pg_prom_exporter_setting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94350.png)

3.  Find your new exporter and view the monitoring dashboard.

    ![pg_prom_mongodb_dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94351.png)


ARMS Prometheus Monitoring enables you to configure exporters through web browsers, and provides ready-to-use monitoring dashboards. Currently, it supports most mainstream database components. More application components will be supported in later versions. Stay tuned for further updates.

**Related topics**  


[What is Prometheus Service?]()

