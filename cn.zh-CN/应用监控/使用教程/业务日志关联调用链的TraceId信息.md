# 业务日志关联调用链的TraceId信息

您可以在应用的业务日志中关联调用链的TraceId信息，从而在应用出现问题时，能够通过调用链的TraceId快速关联到业务日志，及时定位分析、解决问题。

您已将Agent版本升级至2.6.1.2及以上版本，详情请参见[更新Java探针版本](/cn.zh-CN/应用监控/升级探针.md)。

ARMS在业务日志中关联调用链TraceId的功能基于MDC（Mapped Diagnostic Context）机制实现，支持主流的Log4j、Log4j2和Logback日志框架。

## 业务日志关联调用链的TraceId信息

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏中选择**应用监控** \> **应用列表**，在顶部菜单栏选择目标地域，然后在应用列表页面单击目标应用的名称。

3.  在左侧导航栏中单击**应用设置**，并在右侧单击自定义配置页签。

4.  在自定义配置页签的**业务日志关联设置**区域，打开**关联业务日志与TraceId**。

    ![sc_am_log_correlation](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4796310061/p94135.png)

    **说明：**

    -   开启此开关后，会在业务日志中自动生成调用链的TraceId。
    -   如果您还需要绑定Project和Logstore，实现精准定位业务异常问题，详情请参见[t1949734.md\#]()。
5.  在您业务日志的Layout的Pattern属性中添加`%X{EagleEye-TraceID}`配置。以Logback组件添加此配置为例，如下图所示。

    ![dg_am__layout_pattern](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6870348951/p94145.png)

6.  重启应用。

    在应用的业务日志中成功打印出TraceId信息，则说明业务日志关联调用链的TraceId关联成功，如下图所示。

    ![dg_am_log_traceid](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6870348951/p94151.png)


