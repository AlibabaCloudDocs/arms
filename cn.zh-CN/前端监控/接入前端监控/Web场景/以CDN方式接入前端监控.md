# 以CDN方式接入前端监控

要使用ARMS前端监控子产品监控Web应用，必须先以CDN或npm方式安装探针。本文介绍如何以CDN方式为Web应用安装ARMS前端监控探针。

## 安装前端监控探针

1.  登录[ARMS控制台](https://arms.console.aliyun.com/#/home)。

2.  在左侧导航栏中单击**前端监控**，在前端监控页面右上角单击**创建应用站点**。

3.  在**创建应用站点**对话框中，选择监控类型Web，输入应用名称，并单击**确定**。

    ![Dialog Box Create New Site](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8178338951/p43513.png)

4.  在应用的应用设置页面的**SDK扩展配置项**区域选中需要的选项，便于快捷生成待插入页面的BI探针代码。

    -   **关闭API自动上报**：选中此项后，需手动调用`__bl.api()`方法上报API成功率。
    -   **开启SPA自动解析**：选中此项后，ARMS会监听页面的`hashchange`事件并自动上报PV，适用于SPA（Single-Page Application，单页面应用）场景。
    -   **开启首屏FMP采集**：选中此项后，ARMS将采集首屏FMP（First Meaningful Paint，首次有效渲染）数据。
    -   **开启页面资源上报**：选中此项后，在页面onload事件触发时会上报页面加载的静态资源。
    -   **与应用监控关联**：选中此项后，API请求会与后端应用监控进行端到端关联。
    -   **开启用户行为回溯**：选中此项后，JS错误诊断可提供用户行为回溯。
    -   **开启Console追踪**：开启此项后，用户行为回溯会追踪Console内容，包括`error`、`warn`、`log`、`info`等。

        **说明：** 此功能会影响Console的路径。

5.  选择以下方法之一来安装前端监控探针。

    -   异步加载：复制提供的代码并粘贴至页面HTML中`<body>`元素内部的第一行，然后重启应用。

        ![tab_bm_async_load](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8178338951/p120732.png)

    -   同步加载：复制提供的代码并粘贴至页面HTML中`<body>`元素内部的第一行，然后重启应用。

        ![tab_bm_sync_load](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8178338951/p120734.png)

    -   npm包：
        1.  执行以下命令以引入npm包。

            ```
            npm install alife-logger --save
            ```

        2.  从控制台上复制以下初始化命令并执行。

            ```
            const BrowserLogger = require('alife-logger');
            const __bl = BrowserLogger.singleton({pid:"b590lhguqs@8cc3f63543d****",appType:"web",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?",sendResource:true,behavior:true,enableLinkTrace:true,enableConsole:true});
            ```


## 异步加载和同步加载方式的区别

-   异步加载：又称为非阻塞加载，表示浏览器在下载执行JS之后还会继续处理后续页面。若对页面性能的要求非常高，建议使用此方式。

    **说明：** 由于是异步加载，ARMS无法捕捉到监控SDK加载初始化完成之前的JS错误和资源加载错误。

-   同步加载：又称为阻塞加载，表示当前JS加载完毕后才会进行后续处理。如需捕捉从页面打开到关闭的整个过程中的JS错误和资源加载错误，建议使用此方式。

## 自定义UID

使用同步加载或异步加载方式安装ARMS前端监控探针时，Web端SDK会自动生成UID来统计UV等信息。自动生成的UID可以用来区分用户的标识，但不具有业务属性，如需自定义UID，请在上述代码`config`中加入以下内容：

```
uid: "xxx" // 该值用于区分用户的标识，根据业务设置。
```

例如：

```
<script>
!(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",appType:undefined,imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", uid: "xxxx"};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>
```

**说明：** 如果更改了上一步的SDK扩展配置项，代码将会发生变化，请务必重新复制粘贴。

## 通用SDK配置项

ARMS前端监控提供一系列SDK配置项，让您能够通过设置参数来满足额外需求。以下是适用于本文场景的通用配置项。

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|pid|String|项目唯一ID，由ARMS在创建站点时自动生成。|是|无|
|uid|String|用户ID，用于标识访问用户，可手动配置，用于根据用户ID检索。如果不配置，则由SDK自动生成且每半年更新一次。|否|由SDK自动生成|
|tag|String|传入的标记，每条日志都会携带该标记。|否|无|
|release|String|应用版本号。建议您配置，便于查看不同版本的上报信息。|否|`undefined`|
|environment|String|环境字段，取值为：prod、gray、pre、daily和local，其中： -   prod表示线上环境。
-   gray表示灰度环境。
-   pre表示预发环境。
-   daily表示日常环境。
-   local表示本地环境。

|否|`prod`|
|sample|Integer|日志采样配置，值为1~100的整数。对性能日志和成功API日志按照`1/sample`的比例采样，关于性能日志和成功API日志的指标说明，请参见[统计指标说明](/cn.zh-CN/前端监控/统计指标说明.md)。|否|`1`|
|behavior|Boolean|是否为了便于排查错误而记录报错的用户行为。|否|`true`|
|enableSPA|Boolean|监听页面的hashchange事件并重新上报PV，适用于单页面应用场景。|否|`false`|
|enableLinkTrace|Boolean|进行前后端链路追踪，请参见[t152278.md\#](/cn.zh-CN/前端监控/使用教程/使用前后端链路追踪诊断API错误原因.md)。|否|`false`|

ARMS前端监控还提供了更多SDK配置项，可满足进一步的需求，具体操作，请参见[SDK参考](/cn.zh-CN/前端监控/SDK参考.md)。

**相关文档**  


[前端监控接入概述](/cn.zh-CN/前端监控/接入前端监控/前端监控接入概述.md)

[SDK参考](/cn.zh-CN/前端监控/SDK参考.md)

[以npm方式接入前端监控](/cn.zh-CN/前端监控/接入前端监控/Web场景/以npm方式接入前端监控.md)

[在Weex环境接入前端监控](/cn.zh-CN/前端监控/接入前端监控/Weex场景/在Weex环境接入前端监控.md)

