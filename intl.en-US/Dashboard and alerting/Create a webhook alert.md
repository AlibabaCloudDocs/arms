# Create a webhook alert

After you configure a webhook alert, you can send alert notifications to a custom webhook address by using a specified method.

## Create a webhook alert

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the Contact tab, click **Create a webhook** in the upper-right corner.

4.  In the **Create Webhook** dialog box, set the required parameters.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Webhook Name|Required. The custom webhook name.|
    |Post and Get|Required. Set the request method. The URL cannot exceed 100 characters.|
    |Header and Param|Optional. Set the request header. The length cannot exceed 200 characters. Click **Add** to add a header or parameter. The default request header is Content-Type: text/plain; charset=UTF-8. A maximum of six headers and parameters can be created.|
    |Body|Optional. This parameter is displayed in the POST method. The $content placeholder can be used in the Body string to output alert content. The length cannot exceed 500 characters.|

5.  Click **Test** to verify whether the configuration is successful.

6.  Click **Create**.


**Note:** The timeout period of a webhook alert is five seconds. If the webhook receives no response within five seconds after a notification request is sent, the notification request fails.

