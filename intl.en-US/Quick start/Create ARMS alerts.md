# Create ARMS alerts

Application Real-Time Monitoring Service \(ARMS\) allows you to create alerts for monitoring jobs. When alert conditions are met, you can receive alerts in real time through emails, SMS messages, and DingTalk. This helps you detect errors in a proactive manner. This topic describes how to create application monitoring alerts, browser monitoring alerts, custom monitoring alerts, and Prometheus monitoring alerts by using an instance.

## Prerequisites

A monitoring job and a contact group are created. For more information, see the following topics:

-   [Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)
-   [Create a contact](/intl.en-US/Dashboard and alerting/Create contacts.md)
-   [t1918101.md\#]()

## Create an application monitoring alert

To create a Java Virtual Machine-Garbage Collection \(JVM-GC\) alert for an application monitoring job, perform the following steps:

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/#/home). In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.
2.  On the Alarm Policies page, choose **Create Alarm** \> **Application Monitoring Alarm** in the upper-right corner.
3.  In the **Create Alarm** dialog box, set all the required parameters and click **Save**.

    Set the following parameters:

    ![Create an alert](../images/p127257.png)

    1.  Enter an alert name, for example, JVM-GC\_Comparison.
    2.  In the **Application Site** field, select the monitoring job you created.
    3.  In the **Type** field, select the type of the monitoring metric, for example, JVM\_Monitoring.
    4.  Set Dimension to Traverse.
    5.  Configure an alert rule.
        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of JVM\_FullGC increases by 100% compared with that in the previous hour.

            **Note:** To add another alert rule, click the plus sign \(+\) on the right of the first alert rule.

    6.  Select one or more notification methods. For example, select Email.
    7.  Select the notification receivers. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

## Create a browser monitoring alert

To create a Page\_Metric alert to monitor JS\_Error\_Rate and JS\_Error\_Count for a browser monitoring job, perform the following steps:

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alarm Policies page, choose **Create Alarm** \> **Browser Monitoring Alarm** in the upper-right corner.

3.  In the **Create Alarm** dialog box, set all the required parameters and click **Save**.

    Set the following parameters:

    ![Create a browser monitoring alert](../images/p127262.png)

    1.  Enter an alert name, for example, Page\_Metric.
    2.  In the **Application Site** field, select the monitoring job you created.
    3.  In the **Type** field, select the type of the monitoring metric, for example, Page\_Metric.
    4.  Set Dimension to Traverse.
    5.  Configure an alert rule.
        1.  Select **Meet All of the Following Criteria**.
        2.  Edit the alert rule. For example, an alert is triggered when the value of N is 10 and the average value of JS\_Error\_Rate equals or exceeds 20.
        3.  To add another alert rule, click the plus sign \(**+**\) on the right of the first alert rule. For example, an alert is triggered when the value of N is 10 and the sum of JS\_Error\_Count equals or exceeds 20.
    6.  Select one or more notification methods. For example, select SMS and Email.
    7.  Select the notification receivers. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

## Create a Prometheus monitoring alert

To create an alert on network receiving pressure for a Prometheus monitoring job, perform the following steps:

1.  In the left-side navigation pane, choose **Alerts** \> **Alert Policies**.

2.  On the Alarm Policies page, choose **Create Alarm** \> **Prometheus** in the upper-right corner.

3.  In the **Create Alarm** dialog box, set all the required parameters and click **Save**.

Set the following parameters:

![Create a Prometheus monitoring alert](../images/p127264.png)

1.  Enter an alert name, for example, Received\_Bytes.
2.  Select the **cluster** of the Prometheus monitoring job.
3.  Set **Type** to **grafana**.
4.  Select the specific **dashboard** and **chart**.
5.  Configure an alert rule.
    1.  Select **Meet All of the Following Criteria**.
    2.  Edit the alert rule. For example, an alert is triggered when the value of N is 5 and the average value of Received\_Bytes \(MB\) equals or exceeds 3.

        **Note:** A Grafana chart may contain data of curve A, curve B, and curve C. You can select one of them to monitor.

    3.  In the **PromQL** field, edit or enter a new PromQL statement.

        **Note:** If a PromQL statement contains a dollar sign \(`$`\), an error may occur. You must delete the equal sign \(`=`\) and the parameters on both sides of the equal sign \(`=`\) in the statement that contains the dollar sign \(`$`\). For example, change `sum (rate (container_network_receive_bytes_total{instance=~"^$HostIp.*"}[1m]))` to `sum (rate (container_network_receive_bytes_total[1m]))`.

6.  Select one or more notification methods. For example, select SMS.
7.  Select the notification receivers. In the **Contact Groups** section, click the name of a contact group. If the contact group appears in the **Selected Groups** section, the setting is successful.

