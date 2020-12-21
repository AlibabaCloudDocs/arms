# 创建Webhook报警

设置Webhook报警后，您可以将告警通知以指定方式发送到自定义的Webhook地址中。

## 创建Webhook报警

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏选择**报警管理** \> **联系人管理**。

3.  在联系人页签上，单击右上角的**新建Webhook**。

4.  在**新建Webhook**对话框中输入配置信息。基本参数描述如下所示。

    |参数|说明|
    |--|--|
    |Webhook配置名|必填|
    |请求方法|必填，支持Post和Get请求方法，URL不可超过100个字符。默认请求头为Content-Type: text/plain; charset=UTF-8。|
    |Header和Param|非必填，不可超过200个字符，Header和Param个数总数不能超过6个。 单击**+添加**，您可以添加Header信息或Param信息。|
    |Body|非必填，在Post方法下出现，可以填任意文本，其中$content会被替换为报警内容，不可超过500个字符。|

5.  单击**测试**，您可以测试Post或Get请求方法是否配置成功。

6.  单击**确认**。


**说明：** Webhook报警的超时时间为5秒，如果发出请求后5秒内没有返回，则表示发送失败。

