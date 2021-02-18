# 为函数计算中的Java应用安装探针

只需安装ARMS应用监控组件（探针），即可对部署在函数计算中的Java应用进行监控，查看应用拓扑、接口调用、异常事务和慢事务等方面的监控数据。本文介绍如何为函数计算中的Java应用安装探针。

[使用控制台创建函数]()

## 获取License Key

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
2.  在应用列表页面顶部选择目标地域，在右上角单击**接入应用**。
3.  在接入应用页面顶部单击License Key右侧的复制图标保存License Key值。

    ![Section LicenseKey](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9141208061/p45312.png)


## 操作步骤

1.  登录[函数计算控制台](https://fc.console.aliyun.com)。

2.  在顶部菜单栏，选择地域。

3.  在左侧导航栏中，单击**服务及函数**。

4.  在服务列表区域单击目标服务。

5.  在函数列表页签找到目标函数，单击操作列的**修改配置**。

6.  在修改配置页面，设置环境变量为键值。

7.  设置键为FC\_EXTENSIONS\_ARMS\_LICENSE\_KEY，值为[获取License Key](#section_h12_i6i_iti)中获取的LicenseKey，然后单击**提交**。

    ![FC中的java接入ARMS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2655108061/p200496.png)


## 结果验证

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
2.  在应用列表页面顶部选择目标地域。

在[函数计算控制台](https://fc.console.aliyun.com)多次调用该函数后，若Java应用出现在应用列表中且有数据上报，则说明接入成功。

## 更多信息

**相关文档**  


[使用控制台创建函数]()

