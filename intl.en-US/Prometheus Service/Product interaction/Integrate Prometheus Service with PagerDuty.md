# Integrate Prometheus Service with PagerDuty

PagerDuty is a software solution that helps IT departments of enterprises respond to events. You can integrate Prometheus Service with PagerDuty to enable automatic event notifications or track service changes.

-   Your Kubernetes cluster is monitored by Prometheus Service. For more information, see [Get started with Prometheus Service]().
-   An alert rule is created and enabled. For more information, see [Create an alert]().

PagerDuty is a software solution that helps IT departments of enterprises respond to events. When an event occurs, PagerDuty can alert IT departments by using phone calls, text messages, or emails. For more information about PagerDuty, visit the [official website of PagerDuty](https://www.pagerduty.com/company/).

## Procedure

The following figure shows the procedure for integrating Prometheus Service with PagerDuty.

![flow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2672537161/p249807.png)

## Step 1: Create a PagerDuty account

To create a PagerDuty account with a 14-day free trial, perform the following steps:

1.  Go to the [sign-up page of PagerDuty](https://www.pagerduty.com/sign-up/).

2.  In the **Try PagerDuty** section, perform the following steps:

    1.  Enter an email address and click **GET STARTED!**.

    2.  Enter a name and click **NEXT STEP**.

    3.  Enter a password and click **NEXT STEP**.

    4.  Enter a subdomain, select the check box for the Terms of Service and Privacy Policy, and then click **CREATE ACCOUNT**.

    After the account is created, the PagerDuty welcome page appears.

    ![Welcome](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2672537161/p249199.png)


## Step 2: Create a service

To create a service for Prometheus Service in the PagerDuty console, perform the following steps:

1.  Log on to the [PagerDuty console](https://app.pagerduty.com/).

2.  In the top navigation bar, choose **Services** \> **Service Directory**.

3.  On the **Service Directory** page, click **New Service**.

4.  On the **Add a Service** page, enter a service name, select **Prometheus** from the **Integration Type** drop-down list, and then click **Add Service**.

    **Note:** You can also set other parameters for your service based on your business requirements.

    After the service is created, the details page of the service appears, as shown in the following figure.

    ![service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5945188161/p249259.png)


## Step 3: Obtain the integration key

To obtain the key that is used to integrate Prometheus Service with PagerDuty, perform the following steps:

1.  On the details page of the service, click the **Integrations** tab.

2.  On the **Integrations** tab, find Prometheus and click the Copy to clipboard icon in the **Integration Key** column.

    ![integration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2672537161/p249295.png)


## Step 4: Create a contact

To use the integration key to create a contact, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the **Contact Management** page, click **New contact**.

4.  In the **New contact** dialog box, specify a contact name, enter the integration key in the **DingTalk robot** field, and then click **OK**.

    ![contact](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3672537161/p249309.png)


## Step 5: Create a notification policy

To create a notification policy for the contact, perform the following steps:

1.  Log on to the [Prometheus console](https://prometheus.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Notification Policies**.

3.  On the **Notification Policies** page, click **Create Policy** in the **Alert Policies** section.

4.  On the right of the **Notification Policies** page, enter a name for the notification policy. In the **Event Processing** section, set the **Processing Method** parameter to **Generate alerts**. In the **Alert Notification** section, select your contact from the **Contact** drop-down list, set the **Notification Method** parameter to **DingTalk**, specify a time period during which notifications can be sent, and then click the check mark in the upper-right corner.


## Step 6: Modify an alert rule

To change the notification policy of an alert rule to the policy that you created, perform the following steps:

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar of the **Prometheus Monitoring** page, select a region. Then, click the name of the Kubernetes cluster that you want to manage.

4.  In the left-side navigation pane, click **Alert configuration**.

5.  On the Alert configuration page, find the alert rule that you want to modify and click **Editing** in the **Actions** column.

6.  In the **Edit alarm** panel, select the notification policy that you created from the **Notification Policy** drop-down list and click **OK**.


## Verify the integration

You can view alerts in the PagerDuty console to check whether Prometheus Service is integrated with PagerDuty.

1.  Log on to the [PagerDuty console](https://app.pagerduty.com/).

2.  In the top navigation bar, choose **Incidents** \> **Alerts**.

    The **Alerts on All Teams** page displays triggered alerts, as shown in the following figure.

    ![Alerts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3672537161/p249804.png)

3.  If you want to view the details of an alert, find the alert and click the name of the alert in the **Summary** column.


