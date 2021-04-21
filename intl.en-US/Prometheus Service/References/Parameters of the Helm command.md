# Parameters of the Helm command

Helm is provided for installing ARMS Prometheus Monitoring Operator. This article introduces the parameters of the Helm command used during the process.

Here is an example of the Helm command used during the installing process:

```
helm install arms-prom-operator aliyun/ack-arms-prometheus \
                --install \
                --version 0.1.5 \
                -- namespace arms-prom \
                -- set controller.cluster_id=123 \
                -set controller.uid="456" \
                -set controller.region_id=eu-central-1 \
                -- set controller.operatorImage=registry-vpc.eu-central-1.aliyuncs.com/arms-docker-repo/arms-prom-operator:v0.1 \
                -- set controller.kubeStateMetric=registry-vpc.eu-central-1.aliyuncs.com/acs/kube-state-metrics:v1.6.0 \
                -- set controller.nodeExportorImage=registry-vpc.eu-central-1.aliyuncs.com/acs/node-exporter:v0.17.0
```

|Parameter|Description|
|---------|-----------|
|version|Helm version|
|namespace|Target Helm namespace|
|controller.cluster\_id|Cluster ID of the current Kubernetes cluster|
|controller.uid|User ID of the Alibaba Cloud account|
|controller.region\_id|Region ID of the current Kubernetes cluster|
|controller.operatorImage|Image address of ARMS Prometheus agent, each region has one VPC|
|controller.kubeStateMetric|Image address of KubeStateMetrics, each region has one VPC|
|controller.nodeExportorImage|Image address of NodeExporter, each region has one VPC|

