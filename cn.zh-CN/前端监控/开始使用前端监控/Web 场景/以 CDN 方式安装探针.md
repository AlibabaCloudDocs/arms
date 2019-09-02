# 以 CDN 方式安装探针 {#concept_58663_zh .task}

要使用 ARMS 前端监控监控 Web 应用，必须先以 CDN 或 npm 方式安装探针。本文介绍如何以 CDN 方式为 Web 应用安装 ARMS 前端监控探针。

1.  登录[ARMS 控制台](https://arms-intl.console.aliyun.com/#/home)，在左侧导航栏中选择**应用监控** \> **应用列表**。
2.  在左侧导航栏中选择**前端监控**，在前端监控页面右上角单击**新建应用站点**。
3.  在**新建应用站点**对话框中，选择站点类型 Web，输入站点名称，并单击**确定**。 

    ![Dialog Box Create New Site](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152261/156741145143513_zh-CN.png)

4.  在应用的设置页面的 **SDK 扩展配置项**区域勾选需要的选项。 
    -   关闭 API 自动上报：勾选此项后，需手动调用 `__bl.api()` 方法上报 API 成功率。
    -   开启 SPA 自动解析：勾选此项后，ARMS 会监听页面的 hashchange 事件并自动上报 PV，适用于 SPA（Single-Page Application，单页面应用）场景。
    -   开启首屏 FMP 采集：勾选此项后，ARMS 将采集首屏 FMP（First Meaningful Paint，首次有效渲染）数据。
    -   开启页面资源上报：勾选此项后，在页面 onload 事件触发时会上报页面加载的静态资源。
    -   与应用监控关联：勾选此项后，API 请求会与后端应用监控进行端到端关联。
5.  在**复制/粘贴BI探针**区域，复制提供的代码并粘贴至页面 HTML 中 `<body>` 元素内部的第一行，然后重启应用。 

    ![Section Install BI Agent](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152261/156741145243515_zh-CN.png)

    使用 CDN 方式安装 ARMS 前端监控探针时，Web 端 SDK 会自动生成 UID 来统计 UV 等信息。自动生成的 UID 可以用来区分用户的标识，但不具有业务属性，若您想自定义 UID，请在上述代码 `config` 中加入以下内容：

    ``` {#codeblock_on3_hsc_k1e}
    uid: 'xxx', // 该值用于区分用户的标识，根据业务设置
    ```

    例如：

    ``` {#codeblock_qwv_3e7_miv}
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",appType:undefined,imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", uid: "xxxx"};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>
    ```

    **说明：** 如果更改了上一步的 SDK 扩展配置项，代码将会发生变化，请务必重新复制粘贴。


ARMS 前端监控还提供了更多 SDK 配置项，可满足进一步的需求，请参考[前端监控 SDK 配置项](intl.zh-CN/前端监控/高级选项/前端监控 SDK 配置项.md#)。

[前端监控接入概述](intl.zh-CN/前端监控/开始使用前端监控/前端监控接入概述.md#)

[前端监控 SDK 配置项](intl.zh-CN/前端监控/高级选项/前端监控 SDK 配置项.md#)

[以 npm 方式安装探针](intl.zh-CN/前端监控/开始使用前端监控/Web 场景/以 npm 方式安装探针.md#)

[Weex 接入配置](intl.zh-CN/前端监控/开始使用前端监控/Weex 场景/Weex 接入配置.md#)

