# Basic metrics

When you use Prometheus Monitoring, you are charged based on the number of reported metrics. Prometheus Monitoring supports two types of metrics: basic metrics and custom metrics. Basic metrics are free of charge. Custom metrics are charged as of January 6, 2020.

The following table lists the jobs that can collect basic metrics from Prometheus Monitoring.

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
|API server|\_arms-prom-kube-apiserver|
|apiserver|
|\_arms-prom/kube-apiserver/0|
|Static Kubernetes YAML file|\_kube-state-metrics|
|Ingress|arms-ack-ingress|
|ingress|
|CoreDNS|arms-ack-coredns|
|coredns|

You can view the jobs that collect basic metrics on the Health Check page of Prometheus Monitoring.

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, click **Prometheus Monitoring**.
3.  In the upper-left corner of the Prometheus Monitoring page, select a region and click the name of the Kubernetes cluster that you want to view.
4.  In the left-side navigation pane, click **Health Check**.
5.  On the Health Check Result page, view the started jobs in Step 4 of the check result. To determine whether a job collects basic metrics, check whether the job is free of charge. If a job is free of charge, the job collects basic metrics.

