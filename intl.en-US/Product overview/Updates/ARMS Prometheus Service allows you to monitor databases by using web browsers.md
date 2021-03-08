# ARMS Prometheus Service allows you to monitor databases by using web browsers

An update of Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring is released on March 20, 2020. The new version allows you to connect Redis, MySQL, Elasticsearch, and MangoDB databases to ARMS Prometheus Monitoring and then monitor these databases with a few clicks. Out-of-the-box dashboards are also provided.

**Note:** You can use ARMS Prometheus Monitoring free of charge for 15 days. Click to start your [free trail](https://common-buy.aliyun.com/?&commodityCode=arms#/open). You can join the DingTalk group for free trial users: 23155358.

## Overview of ARMS Prometheus Monitoring

ARMS Prometheus Monitoring provides one-stop, out-of-the-box Prometheus monitoring services that have the following features:

-   Simplified and stable Prometheus collectors: Prometheus collectors are deployed on your cluster by using Helm charts. Based on simplified and optimized Prometheus servers, Prometheus collectors focus on service detection and data collection. The resource consumption of a Prometheus collector is reduced to 5% of the resource consumption of a Prometheus server. Prometheus collectors support horizontal scaling.
-   Stable and large-capacity cloud storage: Cloud storage is based on Alibaba Cloud Log Service and provides unlimited distributed storage space. This ensures high efficiency and stability.
-   Efficient and powerful data query in the cloud: Prometheus servers in the cloud support metric query that is fully compatible with PromQL. In addition, Prometheus servers allows you to sample and speed up queries.
-   Default alerting service: ARMS Prometheus Monitoring supports native alert rules and provides multiple alert notification methods by default, such as emails and DingTalk. Alert notifications can be sent to relevant contacts by using the cloud monitoring service.
-   Out-of-the-box monitoring dashboards for Grafana Cloud: By default, ARMS Prometheus Monitoring provides monitoring dashboards for Kubernetes clusters. This allows you to monitor hosts, pods, deployments, API servers, Ingress, and coreDNS. ARMS Prometheus Monitoring also provides monitoring dashboards for various third-party components.

For more information about ARMS Prometheus Monitoring, see [What is Prometheus Service?]().

## One-click database monitoring

ARMS Prometheus Monitoring supports one-click access to monitor mainstream databases. To view your database monitoring dashboard, perform the following steps:

1.  Select the type of the database that you want to monitor.

    Only Redis, MySQL, Elasticsearch, and MangoDB databases are supported.

    ![pg_prom_choose_database](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94349.png)

2.  Set the parameters for the database that you want to monitor.

    Take MangoDB as an example. Enter the exporter name, connect string, port number, username, and password of the MangoDB database.

    ![pg_prom_exporter_setting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94350.png)

3.  Find your new exporter and view the monitoring dashboard.

    ![pg_prom_mongodb_dashboard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2872684951/p94351.png)


ARMS Prometheus Monitoring enables you to configure exporters through web browsers, and provides ready-to-use monitoring dashboards. ARMS Prometheus Monitoring supports most mainstream database components. More application components will be supported in later versions. Stay tuned for further updates.

**Related topics**  


[What is Prometheus Service?]()

