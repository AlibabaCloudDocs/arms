---
keyword: [auto scaling, collector]
---

# Horizontal pod scaling \(HPA\)

Alibaba Cloud Prometheus supports auto scaling of collectors based on persistent key status.

## Terms

-   Container: provides a type of environment where applications run, such as Kubernetes.
-   Collector: indicates a process that is used to collect monitoring data of applications.
-   HPA: extends the number of machines \(replicas\) for a process in a container.
-   Number of replicas: indicates the number of machines that run a process.

## Background information

An insufficient number of replicas are configured for a Prometheus collector. Therefore, the collector continually runs out of buffer space and restarts. To resolve the issue, Alibaba Cloud Prometheus provides the HPA feature. This feature can automatically adjust the number of replicas for the collector.

## Comparison between Alibaba Cloud Prometheus HPA and open source Kubernetes HPA



Process: An HPA collector collects various metrics data, such as memory usage. If a collected metric value exceeds the threshold that is set for the metric, auto scaling is initiated. For example, you can set the threshold of memory usage to 75%. If the threshold is exceeded, auto scaling occurs.

Disadvantages:

-   You must specify a metric based on which a pod is scaled, such as memory usage or number of requests. This metric is not easy to identify, and the threshold of the metric is set based on experience.
-   You must specify an interval to detect external processes. However, in some scenarios, processes run in a short period and the collector cannot capture metric data.

Processes:

1.  An Alibaba Cloud Prometheus HPA collector runs in a container with only one replica.
2.  If the size of data to be collected is too large, the collector continually runs out of buffer space and restarts.
3.  Each time the collector is restarted, the cause of the restart is detected. If the collector is OOM killed, a request for auto scaling is sent to the ARMS console.
4.  The ARMS console sends a request of adding replicas to Kubernetes. A maximum of 10 replicas can be added.
5.  The ARMS console sends a command of restarting all collectors to Kubernetes. This way, the OOMKilled state that causes the last restart is cleared. The load balancing feature is enabled for collection tasks.

Benefits:

-   Alibaba Cloud Prometheus HPA allows you to identify a metric based on the OOMKilled state.
-   The OOMKilled state is recorded in Kubernetes. You can check whether auto scaling is required based on the Kubernetes status when the collector is started. This allows you to retrieve the status of metrics in a short period.

