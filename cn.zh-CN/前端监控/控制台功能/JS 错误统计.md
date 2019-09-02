# JS 错误统计 {#concept_91589_zh .concept}

本文介绍了 ARMS 前端监控的 JS 错误统计功能。

## JS 错误率的定义是什么？ {#section_wbt_lxq_gfb .section}

在 ARMS 前端监控中，JS 错误率的计算公式为：

```
JS 错误率 = 指定时间内发生 JS 错误的 PV / 总 PV 
```

## 错误率排行 { .section}

在左侧的错误率排行标签页上，列出的是站点内错误率最高或最低的前 100 个页面，可以按照错误率升序或降序排列。右侧的 **JS 错误率图表**展示的是左侧列表选中页面在指定时间范围内的 JS 错误率曲线和 PV。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943633_zh-CN.png)

**说明：** 由于错误率排行榜仅会展示错误率最高或最低的前 100 个页面，当站点的页面总数超过 200 个时，错误率不属于这两个区间的页面始终不会显示在排行中。例如，假设站点共有 220 个页面，那么无论选择按错误率升序还是降序排列，都会有 20 个页面不会显示在排行中。

## 错误聚类排行 { .section}

在左侧的错误聚类排行标签页上，列出的是每种错误信息的发生次数排行。右侧的 JS 错误调用页面展示的是出现了左侧列表选中错误的页面，按错误次数降序排列。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943634_zh-CN.png)

## 地理分布 { .section}

在**地理分布**模块，您可以查看上述统计信息的地理分布情况。地理分布又分为中国和世界两个维度，中国维度的单位为省，世界维度的单位为国家/地区。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943635_zh-CN.png)

## 终端分布 { .section}

在**终端分布**模块中，您可以查看上述统计信息的终端分布情况。终端分布又细分为浏览器、操作系统、设备、分辨率等维度。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943638_zh-CN.png)

## 通用操作 { .section}

在 JS 错误统计模块中，您可以执行以下通用操作。

-   在左侧标签页上，单击标签上的上箭头或下箭头来改变列表的排列顺序。上箭头表示升序，下箭头表示降序。

-   在右侧的详情显示区域中，单击右上角的列表图标，可在图表和表格视图间切换。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943639_zh-CN.png)

-   在右侧的详情显示区域中，单击右上角的时钟图标，可指定时间范围。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943644_zh-CN.png)


## 如何进行 JS 错误排查？ {#section_j5c_fjh_hfb .section}

您可通过以下操作进入**JS 错误详情**页面。

1.  单击左侧导航栏中JS 错误率标签页。

2.  在JS 错误率标签页选择需排查的对象，并单击**JS 错误类聚**区域的**明细**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943646_zh-CN.png)

    JS 错误详情页面打开。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742464943647_zh-CN.png)

    **说明：** 若信息过长显示不完整，将鼠标移到错误信息外即可显示全部信息。


在JS 错误详情页可查看错误明细，根据每条错误上的关键信息，即可定位到 JS 错误所在的文件和信息，帮助前端工程师快速定位问题。

每条错误可显示的关键信息：

-   上报时间

-   日志类型

-   页面地址

-   浏览器

-   设备

-   地域

-   Tag

-   UA\(User Agent\)

-   Param 参数

-   Message\(信息）

-   Stack\(错误栈信息\)

-   File\(错误文件\)

-   Line/Col\(错误位置）


Js 错误详情页还提供了错误搜索功能，搜索条件包括：

-   日志类型：默认是 JS 错误日志

-   时间选择：错误产生的时间

    **说明：** 为提高搜索效率，时间跨度不宜太短。

-   关键字：根据 Message 的关键词进行搜索

    **说明：** 目前只支持全 Message 匹配搜索，暂不支持模糊搜索。


## 如何设置 JS 错误率报警？ { .section}

您可以设置针对 JS 错误率的报警。在以下示例中，触发报警的条件是最近 10 分钟的错误率平均值超过 20%，且最近 10 分钟的错误总数超过 20 个。

1.  在左侧导航栏中选择**设置** \> **报警设置**。

2.  在**设置报警规则**区域单击**新建规则**。

3.  在新建报警对话框中，按照下图输入各项参数。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/152274/156742465043651_zh-CN.png)


## 如何上报资源加载失败的情况（例如 404）？ { .section}

SDK 监控的 JS 错误仅限脚本相关错误，不包括资源加载错误（例如 404）。为防止阻塞业务代码，SDK 会延后加载，因此一般无法捕捉页面加载失败的错误。

如果仍需监控资源失败情况并上报数据，请遵循以下步骤。

1.  在页面 Head 最前面监听 addEventListener onerror 。

    ```
    window.addEventListener("error", function (e) {
    var elem = e.target;
    if(/img|script/.test(elem.tagName.toLowerCase())){
            window.__sourceError = window.sourceError || [];
            window.__sourceError.push(e);
        }
    }, true); /*指定事件处理函数在捕获阶段执行*/
    ```

    **说明：** 第三个参数一定要设为 true。

2.  当 DOM Rready、window.\_\_bl 实例产生后，通过手动方式从 window.\_\_sourceError 解析错误信息。

    ```
    window.__bl && __bl.error(new Error('发生了一个资源加载的错误'), {       filename: '',      })
    // 如果需要方便后台报警设置,可调用 __bl.sum('error-404', 1); 表示某些事件发生的次数。
    ```


关于因跨域资源共享导致的 Script Error，请参考[“Script error.”的产生原因和解决办法](../../../../intl.zh-CN/常见问题/前端监控常见问题/“Script error.”的产生原因和解决办法.md#)。

## 相关文档 { .section}

-   关于因跨域资源共享导致的 Script Error，请参考 [“Script error.”的产生原因和解决办法](../../../../intl.zh-CN/常见问题/前端监控常见问题/“Script error.”的产生原因和解决办法.md#)。

