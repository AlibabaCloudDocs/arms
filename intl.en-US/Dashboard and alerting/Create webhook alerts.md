# Create webhook alerts

After you configure a webhook alert, you can send alert notifications to a specified webhook URL. Prometheus can send Webhook alert notifications to applications such as Feishu, WeChat, and DingTalk. This topic describes how to create a webhook alert. Feishu is used in this example.

## Step 1: Create a webhook URL

1.  Open and log on to Feishu.

2.  Click the **+** icon, and then click **Add Group** to create a Feishu group where alert notifications are sent.

3.  Click the group settings icon, and then click the **Bots** tab.

4.  On the BOTs tab, click **Add Bot**.

    ![Add a bot to a Feishu group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2648758061/p201547.png)

5.  In the Add Bot dialog box, select Custom Bot.

    ![Create a custom bot in Feishu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2648758061/p201572.png)

6.  Set the Bot name and Description parameters, and then click **Next**.

    ![Configure a custom bot in Feishu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2648758061/p201575.png)

7.  Click **Copy** to save the value of the Webhook URL parameter, and then click **Finish**.

    ![Set a webhook URL in Feishu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2648758061/p201577.png)


## Step 2: Create a webhook alert

1.  Log on to the [ARMS console](https://arms-intl.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Alerts** \> **Contacts**.

3.  On the Contact tab, click **Create a webhook** in the upper-right corner.

4.  In the **Create Webhook** dialog box, set the parameters.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Webhook Name|Required. The name of the custom webhook.|
    |Post or Get|Required. The request method. The requested URL cannot exceed 100 characters in length.In this example, select Post and paste the webhook URL that is saved in the [Step 1: Create a webhook URL](#section_8mt_jx4_e7f) section to the field. |
    |Header and Param|Optional. The request header. The header cannot exceed 200 characters in length. You can click **+ Add** to add headers or parameters. The default request header is Content-Type: text/plain; charset=UTF-8. The total number of headers and parameters cannot exceed 6.In this example, set the following two headers:

    -   Arms-Content-Type : json
    -   Content-Type : application/json |
    |Body|Optional. This parameter is available if you use the post method. You can use $content in the body string as a placeholder of alert content. The body cannot exceed 500 characters in length.In this example, use the following alert content format:

    ```
{"msg_type": "text","content": {"text": "$content"}}
    ``` |

5.  Click **Test** to verify whether the configurations are valid.

6.  Click **Create**.


