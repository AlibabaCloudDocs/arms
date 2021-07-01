# Create an alert

Prometheus Service provides out-of-the-box alert rules. You can also customize alert rules for specific monitored objects. If a rule is triggered, the system sends alert messages to the specified contact group by using the specified notification method. This way, contacts can resolve issues at the earliest opportunity.

-   A monitoring task is created. For more information, see [Connect an ACK cluster to Prometheus Service]().
-   Contacts are created. For more information, see [Create a contact](/intl.en-US/Dashboard and Alerting/Create a contact.md).

## Procedure

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select the region where the monitored Kubernetes cluster resides. Then, click the name of the Kubernetes cluster in the K8s column.

4.  In the left-side navigation pane, click **Alarm configuration**.

5.  On the Alarm configuration page, click **Create Alert** in the upper-right corner.

6.  In the **Create Alert** panel, configure the parameters.

    1.  Select a template from the **Alert Template** drop-down list.

    2.  Enter a rule name in the **Rule Name** field. Example: Alert for inbound traffic.

    3.  Enter a PromQL statement as the expression in the **Alert Query** field. Example: `(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`.

        **Note:** If a PromQL statement contains a dollar sign \(`$`\), an error is returned. You must delete the equal sign \(`=`\) and the parameters on both sides of the equal sign \(`=`\) from the statement that contains the dollar sign \($\). For example, change `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`.

    4.  Enter a number in the **Duration** field. Example: 1.

    5.  Enter an alert message in the **Alert Message** field.

    6.  In the **Tag** section of **Advanced Settings**, click **Create Tag** to specify alert tags. The specified tags can be used as options for a dispatch rule.

    7.  In the **Annotation** section of **Advanced Settings**, click **Create Annotation**. Then, enter message in the Key field, and enter \{\{variable name\}\} alert notification in the Value field. The specified annotation is in the format of `message:{{variable name}} alert notification`. Example: `message:{{$labels.pod_name}} restart`.

        You can customize a variable name or select an existing tag as the variable name. Existing tags:

        -   The tags that are carried in the metrics of an alert rule expression.
        -   The tags that are created when you create an alert rule. For more information, see [Create an alert]().
        -   The default tags provided by ARMS. The following table describes the default tags.

            |Tag|Description|
            |---|-----------|
            |alertname|The name of the alert. The format is <Alert name\>\_<Cluster name\>.|
            |\_aliyun\_arms\_alert\_level|The level of the alert.|
            |\_aliyun\_arms\_alert\_type|The type of the alert.|
            |\_aliyun\_arms\_alert\_rule\_id|The ID of the alert rule.|
            |\_aliyun\_arms\_region\_id|The ID of the region.|
            |\_aliyun\_arms\_userid|The ID of the user.|
            |\_aliyun\_arms\_involvedObject\_type|The subtype of the associated object, for example, ManagedKubernetes or ServerlessKubernetes.|
            |\_aliyun\_arms\_involvedObject\_kind|The type of the associated object, for example, app or cluster.|
            |\_aliyun\_arms\_involvedObject\_id|The ID of the associated object.|
            |\_aliyun\_arms\_involvedObject\_name|The name of the associated object.|

    8.  Click **Confirm**.

    After you create an alert, the Alarm configuration page displays the created alert, as shown in the following figure.

    ![8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5006015261/p245624.png)


