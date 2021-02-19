# LogHub数据源

如果您已经开通日志服务LogHub，则可以在ARMS控制台直接同步LogHub中的数据并作为自定义监控的数据源使用。

-   [提交工单申请开通自定义监控](https://selfservice.console.aliyun.com/ticket/createIndex)
-   [开通日志服务](https://www.aliyun.com/product/sls)
-   [创建Project](/cn.zh-CN/数据采集/准备工作/管理Project.md)
-   [创建Logstore](/cn.zh-CN/数据采集/准备工作/管理Logstore.md)

## 同步LogHub数据源

**说明：** 使用主账号或已被授权访问LogHub的RAM用户登录ARMS控制台。如果使用未被授权访问LogHub的RAM用户登录，则无法授权ARMS访问您在LogHub中的资源，继而无法同步LogHub数据源。

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏，选择**自定义监控数据源管理** \> **LogHub数据源**。

3.  如果此前未授权ARMS读取LogHub数据，则按照ARMS的提示信息完成授权。

    1.  在**提示**对话框，单击**进入RAM进行授权**。

        ![authorize](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3231772161/p43711.png)

    2.  在**云资源访问授权**页面，选择权限，然后单击**同意授权**。

        ![log](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3231772161/p43712.png)

4.  在**实例列表**页面的顶部菜单栏，选择地域，单击**同步LogHub**。

5.  在**同步LogHub**对话框，单击**确定同步**。

    **实例列表**页面显示您在该地域创建的LogStore。

    ![project](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3231772161/p213006.png)


## 更多信息

同步LogHub数据源后，您可以为该数据源创建监控任务。具体操作，请参见[配置数据源](/cn.zh-CN/自定义监控/创建监控任务/配置数据源.md)。

