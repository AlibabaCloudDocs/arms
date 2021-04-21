# Helm命令参数说明

Prometheus支持通过Operator方式安装K8s集群，本文介绍Operator安装过程中的Helm命令的各参数说明。

使用Operator方式安装K8s集群的Helm示例命令如下：

```
helm install arms-prom-operator aliyun/ack-arms-prometheus \
                --install  \
                --version 0.1.5 \
                --namespace arms-prom \
                --set controller.cluster_id=123 \
                --set controller.uid="456" \
                --set controller.region_id=eu-central-1 \
                --set controller.operatorImage=registry-vpc.eu-central-1.aliyuncs.com/arms-docker-repo/arms-prom-operator:v0.1 \
                --set controller.kubeStateMetric=registry-vpc.eu-central-1.aliyuncs.com/acs/kube-state-metrics:v1.6.0 \
                --set controller.nodeExportorImage=registry-vpc.eu-central-1.aliyuncs.com/acs/node-exporter:v0.17.0
```

|参数|说明|
|--|--|
|version|Helm版本。|
|namespace|Helm目标命名空间。|
|controller.cluster\_id|当前K8s所在集群的Cluster ID。|
|controller.uid|阿里云账号的User ID。|
|controller.region\_id|当前K8s所在集群的Region ID。|
|controller.operatorImage|ARMS Prometheus Agent的镜像地址，每一个地域都有一个内网地址。|
|controller.kubeStateMetric|KubeStateMetrics的镜像地址，每一个地域都有一个内网地址。|
|controller.nodeExportorImage|NodeExporter的镜像地址，每一个地域都有一个内网地址。|

