# MQ数据源

本文介绍如何同步消息队列RocketMQ版的Topic作为自定义监控的数据源。

-   [提交工单申请开通自定义监控](https://selfservice.console.aliyun.com/ticket/createIndex)
-   [开通消息队列RocketMQ版]()
-   [创建实例]()
-   [创建Topic]()

关于利用MQ数据源进行监控的案例，请参见[车联网实时监控方案](/cn.zh-CN/产品简介/应用场景/车联网实时监控方案.md)。

## 同步MQ数据源

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**自定义监控数据源管理** \> **MQ数据源**。

3.  如果此前未授权ARMS读取MQ数据，则按照ARMS的提示信息完成授权。

    1.  在**提示**对话框，单击确定授权。

        ![确定授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6231772161/p212658.png)

    2.  在**确认**对话框，单击**确定**。

4.  在**实例列表**页面的顶部菜单栏，选择地域，然后在页面右上角，单击**刷新**。

    **实例列表**页面显示您在该地域创建的消息队列RocketMQ版Topic。

    ![topic](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2382240161/p43716.png)


## 更多信息

同步MQ数据源后，您可以为该数据源创建监控任务。具体操作，请参见[配置数据源](/cn.zh-CN/自定义监控/创建监控任务/配置数据源.md)。

