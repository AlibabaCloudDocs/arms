# SPA页面上报

在SPA（Single Page Application）单页面应用中，页面只会刷新一次。传统的方式只会在页面加载完成后上报一次PV，而无法统计到各个子页面的PV，也无法让其他类型的日志按子页面聚合。本文介绍如何使用ARMS前端监控SDK解决SPA页面上报问题。

ARMS前端监控SDK提供了针对SPA页面的两种处理方式：

-   开启SPA自动解析
-   完全手动上报

## 开启SPA自动解析

此方法适用于大部分以URL Hash作为路由的单页面应用场景。

在初始化的配置项中，设置enableSPA为`true`，即会开启页面的Hashchange事件监听（触发重新上报PV），并将URL Hash作为其他数据上报中的page字段。

与enableSPA配套的还有parseHash，更多信息，请参见[enableSPA](/intl.zh-CN/前端监控/SDK参考.mdsc_enablespa)和[parseHash](/intl.zh-CN/前端监控/SDK参考.md)。

## 完全手动上报

此方法可用于所有的单页面应用场景。如果第一种方法无效，则可用此方法。

SDK提供了setPage方法来手动更新数据上报时的page name。调用此方法时，默认会重新上报页面PV。更多信息，请参见[setPage\(\)](/intl.zh-CN/前端监控/API参考.md)。

```
// 监听应用路由变更事件。
app.on('routeChange', function (next) {
    __bl.setPage(next.name);
});                    
```

**相关文档**  


[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)

[API参考](/intl.zh-CN/前端监控/API参考.md)

