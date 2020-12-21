# Create webhook alerts

After you configure a webhook alert, you can send alert notifications to a custom webhook address in the specified way.

## Create webhook alerts

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the Contact tab, click **Create a webhook** in the upper-right corner.

4.  In the **Create Webhook** dialog box, set configuration parameters. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Webhook Name|Required. An informative name of the webhook alert.|
    |Request method|Required. Valid values: Post and Get. The URL cannot exceed 100 characters in length. The default request header format is Content-Type: text/plain; charset=UTF-8.|
    |Header and Param|Optional. This parameter cannot exceed 200 characters in length. You can configure up to six Headers and Params in total. Click **+ Add** to add Header or Param.|
    |Body|Optional. This parameter takes effect only when the request method is set to Post. Use $content in the body as the placeholder of alert content. The body cannot exceed 500 characters in length.|

5.  Click **Test** to check whether the Post or Get request method is configured.

6.  Click **Create**.


**Note:** If the webhook receives no response within five seconds after a notification request is sent, the notification request fails.

