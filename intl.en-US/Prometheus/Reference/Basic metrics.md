# Basic metrics

Application Real-Time Monitoring Service \(ARMS\) Prometheus Monitoring will charge you based on the number of reported metrics. It supports two types of metrics: basic metrics and custom metrics. Basic metrics are free, and custom metrics are charged starting from January 6, 2020.

The following table describes the basic metric collection jobs supported by ARMS Prometheus Monitoring.

|Job type|Job name|
|--------|--------|
|ARMS Prometheus|\_arms-prom/node-exporter/0|
|node-exporter|
|kubelet information|\_arms/kubelet/metric|
|\_arms-prom/kube-apiserver/metric|
|\_arms-prom/kubelet/0|
|\_arms-prom/kubelet/1|
|Pod CPU|\_arms/kubelet/cadvisor|
|\_arms-prom/kube-apiserver/cadvisor|
|API server|\_arms-prom-kube-apiserver|
|apiserver|
|\_arms-prom/kube-apiserver/0|
|Static Kubernetes YAML file|\_kube-state-metrics|
|Ingress|arms-ack-ingress|
|ingress|
|CoreDNS|arms-ack-coredns|
|coredns|

You can also view the basic metrics collection jobs on the Health Check page of ARMS Prometheus Monitoring.

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Prometheus Monitoring**. On the Prometheus Monitoring page, select a region in the top navigation bar and click the name of the Kubernetes cluster you want to view.
3.  In the left-side navigation pane, click **Health Check**.
4.  On the Health Check Result page, view the collection jobs that have been started in Step 4 in the check result, and determine whether the jobs are used to collect basic metrics based on whether the jobs are free of charge.

    ![Health Check](../images/p75078.png)


