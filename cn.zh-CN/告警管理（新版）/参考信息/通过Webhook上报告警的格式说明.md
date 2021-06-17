# 通过Webhook上报告警的格式说明

通过配置特定的Webhook的Body参数， ARMS在发送Webhook请求时会自动渲染Body，将告警内容通过开源AlertManager的格式进行发送。

## 使用限制

通过Webhook自定义告警通知时，Body参数存在以下使用限制。

-   只能在Body中使用`$alertmanager_content`字段。
-   Content-Type类型必须是application/json。
-   不能和`$content`字段混用，使用`$alertmanager_content`后`$content`不生效。
-   ARMS控制台测试Webhook功能无法对`$alertmanager_content`进行替换测试。

通过Webhook自定义告警通知的操作，请参见[通过Webhook自定义告警通知人](/cn.zh-CN/告警管理（新版）/控制台操作/联系人管理/通过Webhook自定义告警通知人.md)。

## 投递的告警格式

向Webhook投递开源AlertManager格式如下。更多信息，请参见[Prometheus官方文档](https://prometheus.io/docs/alerting/latest/configuration/#webhook_config)。

```
{
  "alerts": [
    {
      "annotations": {
        "_aliyun_arms_alert_value": "15.521240234375",
        "_aliyun_arms_alert_message": "null\n消息ID: ac10c42a16124966960554200d2450-7996494\n",
        "_aliyun_arms_alert_now_value": "15.521240234375",
        "message": "报警：命名空间: {{$labels.namespace}} / Pod: {{$labels.pod_name}} / 容器: {{$labels.container}} 内存使用率超>过80%, 当前值{{ printf \"%.2f\" $value }}%",
        "value": "15.521240234375",
        "_aliyun_arms_alert_past_value": "15.521240234375"
      },
      "endsAt": "2021-02-22T07:27:15.404000000Z",
      "fingerprint": "bec72890cc2c7b4a027e008df0cd1013",
      "labels": {
        "container": "kube-state-metrics",
        "severity": "warning",
        "_aliyun_arms_alert_level": "ERROR",
        "instance": "10.0.80.186:10255",
        "clustername": "klyz1688-kubernetes-1",
        "_aliyun_arms_alert_type": "101",
        "_aliyun_arms_integration_name": "测试集成-prometheus",
        "alertname": "容器内存使用率大于80%",
        "_aliyun_arms_userid": "1131971649496228",
        "_aliyun_arms_involvedObject_name": "klyz1688-kubernetes-1",
        "pod_name": "kube-state-metrics-ccb59dbff-jljg4",
        "_aliyun_arms_involvedObject_id": "cb36dcafb9b9340498fad2e1f40b9a254",
        "_aliyun_arms_region_id": "cn-hangzhou",
        "_aliyun_arms_involvedObject_kind": "cluster",
        "_aliyun_arms_product_type": "PROMETHEUS",
        "name": "k8s_kube-state-metrics_kube-state-metrics-ccb59dbff-jljg4_arms-prom_359508f3-7e76-4740-b915-41ea48849641_0",
        "namespace": "arms-prom",
        "_aliyun_arms_integration_id": "80",
        "_aliyun_arms_involvedObject_type": "ManagedKubernetes",
        "_aliyun_arms_alert_rule_id": "3927051"
      },
      "startsAt": "2021-02-22T07:18:15.578000000Z",
      "status": "firing"
    }
  ],
  "commonAnnotations": {
    "_aliyun_arms_alert_value": "15.521240234375",
    "_aliyun_arms_alert_message": "null\n消息ID: ac10c42a16124966960554200d2450-7996494\n",
    "_aliyun_arms_alert_now_value": "15.521240234375",
    "message": "报警：命名空间: {{$labels.namespace}} / Pod: {{$labels.pod_name}} / 容器: {{$labels.container}} 内存使用率超过80%, 当前值{{ printf \"%.2f\" $value }}%",
    "value": "15.521240234375",
    "_aliyun_arms_alert_past_value": "15.521240234375"
  },
  "commonLabels": {
    "container": "kube-state-metrics",
    "severity": "warning",
    "_aliyun_arms_alert_level": "ERROR",
    "instance": "10.0.80.186:10255",
    "clustername": "klyz1688-kubernetes-1",
    "_aliyun_arms_alert_type": "101",
    "_aliyun_arms_integration_name": "测试集成-prometheus",
    "alertname": "容器内存使用率大于80%",
    "_aliyun_arms_userid": "1131971649496228",
    "_aliyun_arms_involvedObject_name": "klyz1688-kubernetes-1",
    "pod_name": "kube-state-metrics-ccb59dbff-jljg4",
    "_aliyun_arms_involvedObject_id": "cb36dcafb9b9340498fad2e1f40b9a254",
    "_aliyun_arms_region_id": "cn-hangzhou",
    "_aliyun_arms_involvedObject_kind": "cluster",
    "_aliyun_arms_product_type": "PROMETHEUS",
    "name": "k8s_kube-state-metrics_kube-state-metrics-ccb59dbff-jljg4_arms-prom_359508f3-7e76-4740-b915-41ea48849641_0",
    "namespace": "arms-prom",
    "_aliyun_arms_integration_id": "80",
    "_aliyun_arms_involvedObject_type": "ManagedKubernetes",
    "_aliyun_arms_alert_rule_id": "3927051"
  },
  "externalURL": "https://alerts.console.aliyun.com/#/alarm/alert/detail/2848",
  "groupLabels": {
    "alertname": "容器内存使用率大于80%"
  },
  "receiver": "testjiubian",
  "status": "firing"
}
```

