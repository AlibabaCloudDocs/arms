# Basic metrics

You are charged for using Prometheus Service based on the number of reported metrics. The following two types of metrics are supported: basic metrics and custom metrics. Basic metrics are free of charge. Custom metrics are charged after January 6, 2020.

The following table lists the jobs that can collect basic metrics from Prometheus Service.

|Job type|Job name|
|--------|--------|
|Prometheus|\_arms-prom/node-exporter/0|
|node-exporter|
|Kubelet information|\_arms/kubelet/metric|
|\_arms-prom/kube-apiserver/metric|
|\_arms-prom/kubelet/0|
|\_arms-prom/kubelet/1|
|Pod CPU|\_arms/kubelet/cadvisor|
|\_arms-prom/kube-apiserver/cadvisor|
|API Server|\_arms-prom-kube-apiserver|
|apiserver|
|\_arms-prom/kube-apiserver/0|
|Static Kubernetes YAML file|\_kube-state-metrics|
|Ingress|arms-ack-ingress|
|ingress|
|CoreDNS|arms-ack-coredns|
|coredns|

You can view the collection jobs related to basic metrics on the Health Check page of the Prometheus Service console.

1.  Log on to the [Prometheus Service console](https://prometheus.console.aliyun.com/#/home).
2.  In the upper-left corner of the Prometheus Monitoring page, select a region and click the name of Kubernetes cluster that you want to view.
3.  In the left-side navigation pane, click **Health Check**.
4.  On the Health Check Result page, view the collection jobs that have been started in Step 4 of the check result. You can determine whether the jobs are used to collect basic metrics based on whether the jobs are free of charge.

