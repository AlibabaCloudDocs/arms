# Create an alert

Alibaba Cloud Prometheus Service provides out-of-the-box alert rules. You can also customize alert rules for specific monitored objects. If a rule is triggered, the system will send alert messages to the specified contact group by using a specified notification method. This way, contacts can resolve issues at the earliest opportunity.

-   A monitoring job is created. For more information, see [Get started with Prometheus Service]().
-   Contacts are created. For more information, see [Create contacts](/intl.en-US/Dashboard and alerting/Create contacts.md).

## Procedure

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the top navigation bar, select a region. Then, click the name of the Kubernetes cluster that you want to manage.

3.  In the left-side navigation pane, choose **Alarm configuration beta**, and then click **Create Alert** in the upper-right corner.

4.  In the **Create Alert** dialog box, set the following parameters, and then click **OK**.

    **Note:** The **Time** parameter is not supported.

    1.  Enter a name in the **Rule Name** field, for example, network receiving pressure alert.

    2.  Enter an expression that uses a PromQL statement, for example, `(sum(rate(kube_state_metrics_list_total{job="kube-state-metrics",result="error"}[5m])) / sum(rate(kube_state_metrics_list_total{job="kube-state-metrics"}[5m]))) > 0.01`.

        **Note:** The dollar sign \(`"$"`\) in a PromQL statement can cause an error. You must remove the equal sign \(`=`\) and the parameters on both sides of the equal sign \(`=`\) from the statement that contains the dollar sign \($\). For example, change `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`.

    3.  In the Labels section, click **Create Tag** to specify alert tags. The specified tags can be used as options for a dispatch rule.

    4.  In the Annotations section, you can specify a template for alert messages. Click **Create Annotation**, and then set Key to message and Value to \{\{variable name\}\} alert message. The specified annotation is in the format of message:\{\{variable name\}\} alert notification, for example, message:\{\{$labels.pod\_name\}\} restart.

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

    ![Prometheus-Create alarm](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2026378061/p182018.png)


