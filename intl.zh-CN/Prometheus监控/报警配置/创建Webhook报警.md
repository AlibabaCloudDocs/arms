# 创建Webhook报警

设置Webhook报警后，您可以将告警通知以指定方式发送到自定义的Webhook地址中。Prometheus支持对飞书、微信、钉钉等群组发送Webhook报警，本文以飞书为例，介绍如何创建Webhook报警。

## 步骤一：生成Webhook链接

1.  打开并登录飞书。

2.  单击**+**图标，然后单击**创建群组**，新建一个用于发送报警的群组。

3.  单击群组设置图标，然后单击**群机器人**页签。

4.  在群机器人页签单击**添加机器人**。

    ![飞书添加机器人](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1076018061/p201547.png)

5.  在添加机器人面板选择Custom Bot。

    ![飞书-自定义机器人](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1076018061/p201572.png)

6.  在配置页设置显示名称和描述，然后单击**添加**。

    ![飞书-设置机器人](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1076018061/p201575.png)

7.  单击**复制链接**保存添加情况区域的Webhook地址，然后单击**完成**。

    ![飞书-Webhook](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1076018061/p201577.png)


## 步骤二：创建Webhook报警

1.  登录[ARMS控制台](https://arms-intl.console.aliyun.com/)。

2.  在左侧导航栏选择**报警管理** \> **联系人管理**。

3.  在联系人页签上，单击右上角的**新建Webhook**。

4.  在**创建Webhook**对话框中输入配置信息。

    基本参数描述如下所示。

    |参数|说明|
    |--|--|
    |Webhook名称|必填，自定义Webhook名称。|
    |Post和Get|必填，设置请求方法。URL不可超过100个字符。此例中选择Post，并将[步骤一：生成Webhook链接](#section_8mt_jx4_e7f)中保存的Webhook地址粘贴至右侧文本框。 |
    |Header和Param|非必填，设置请求头，不可超过200个字符。 单击**添加**，您可以添加其他Header信息或Param信息。默认请求头为Content-Type: text/plain; charset=UTF-8，Header和Param个数总数不能超过6个。此例中设置以下两个Header：

    -   Arms-Content-Type : json
    -   Content-Type : application/json |
    |Body|非必填，在Post方法下出现，可在Body字符串中使用$content占位符输出报警内容，不可超过500个字符。此例中可以设置如下报警文本格式：

    ```
{"msg_type": "text","content": {"text": "$content"}}
    ``` |

5.  单击**测试**，您可以验证配置是否成功。

6.  单击**创建**。


