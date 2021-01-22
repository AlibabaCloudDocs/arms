# API参考

前端监控SDK开放了部分接口，包括用于上报数据的数据上报类接口和用于修改SDK配置项的方法类接口。

## 本页索引

-   数据上报类接口：[api\(\)](#sc_api) \| [error\(\)](#sc_error) \| [sum\(\)](#sc_sum) \| [avg\(\)](#sc_avg) \| [reportBehavior\(\)](#sc_reportbehavior) \| [performance\(\)](#sc_performance)
-   方法类接口：[setConfig\(\)](#sc_setconfig) \| [setPage\(\)](#sc_setpage) \| [addBehavior\(\)](#section_i3c_5cr_yvr)

## api\(\)

调用api\(\)接口来上报页面的API调用成功率。

SDK默认会监听页面的AJAX请求并调用此接口上报。 如果页面的数据请求方式是JSONP或者其他自定义方法（例如客户端SDK等），可以在数据请求方法中调用api\(\)方法手动上报。

**说明：** 如果要调用此接口，建议在SDK配置项中将disableHook设置为true。更多信息，请参见[disableHook](/intl.zh-CN/前端监控/SDK参考.md)。

api\(\)语法：

```
__bl.api(api, success, time, code, msg)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|api|String|接口名|是|无|
|success|Boolean|是否调用成功|是|无|
|time|Number|接口耗时|是|无|
|code|String/Number|返回码|否|''|
|msg|String|返回信息|否|''|

api\(\)使用示例：

```
var begin = Date.now(),
    url = '/data/getTodoList.json';

$.ajax({
    url: url,
    data: {id: 123456}
}).done(function (result) {
    var time = Date.now() - begin;
    // 上报接口调用成功。
    window.__bl && __bl.api(url, true, time, result.code, result.msg);
}).fail(function (error) {
    var time = Date.now() - begin;
    // 上报接口调用失败。
    window.__bl && __bl.api(url, false, time, 'ERROR', error.message);
});            
```

[\[回到顶部\]](#sc_index)

## error\(\)

调用error\(\)接口来上报页面中的JS错误或使用者想关注的异常。

一般情况下，SDK会监听页面全局的Error并调用此接口上报异常信息，但由于浏览器的同源策略往往无法获取错误的具体信息，此时就需要使用者手动上报。

error\(\)语法：

```
__bl.error(error, pos)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|error|Error|JS的Error对象|是|无|
|pos|Object|错误发生的位置，包含以下3个属性。|否|无|
|pos.filename|String|错误发生的文件名|否|无|
|pos.lineno|Number|错误发生的行数|否|无|
|pos.colno|Number|错误发生的列数|否|无|

error\(\)使用示例1：监听页面的JS Error并上报。

```
window.addEventListener('error', function (ex) {
    // 一般事件的参数中会包含pos信息。
    window.__bl && __bl.error(ex.error, ex);
});            
```

error\(\)使用示例2：上报一个自定义的错误信息。

```
window.__bl && __bl.error(new Error('发生了一个自定义的错误'), {
    filename: 'app.js', 
    lineno: 10, 
    colno: 15
});            
```

[\[回到顶部\]](#sc_index)

## sum\(\)

调用sum\(\)方法，可以自定义上报的日志，它通常被用于统计业务中特定事件发生的次数。通过sum\(\)方法上报的数据，您可以在自定义统计页面查看：

-   自定义事件发生的趋势图。
-   发生该事件的PV或UV统计。
-   维度分布信息。

sum\(\)语法：

```
__bl.sum(key, value)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|key|String|事件名|是|无|
|value|Number|单次累加上报量|否|1|

sum\(\)使用示例：

```
__bl.sum('event-a');
__bl.sum('event-b', 3);
```

[\[回到顶部\]](#sc_index)

## avg\(\)

调用avg\(\)方法，可以自定义上报的日志，它通常被用于计算业务中特定事件发生的平均次数或平均值。通过avg\(\)方法上报的数据，您可以在自定义统计页面查看：

-   自定义事件发生的趋势图。
-   发生该事件的PV或UV统计。
-   维度分布信息。

avg\(\)语法：

```
__bl.avg(key, value)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|key|String|事件名|是|无|
|value|Number|统计上报量|否|0|

avg\(\)使用示例：

```
__bl.avg('event-a', 1);
__bl.avg('event-b', 3);
```

[\[回到顶部\]](#sc_index)

## addBehavior\(\)

调用addBehavior\(\)接口在当前行为队列末尾添加一条自定义用户行为。

SDK维护一条最大长度为100条的用户行为队列，调用addBehavior\(\)接口可在当前行为队列末尾添加一条自定义用户行为，当发生JS Error时上报当前的行为队列，并将队列清空。

**说明：** 您需要在SDK配置中将behavior配置为true，才可调用此参数。

addBehavior\(\)语法：

```
__bl.addBehavior(behavior)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|data|Object|行为数据。包含： -   name：行为名称，String类型，必填，最大长度20字符。
-   message：行为内容，String类型，必填，最大长度200字符。

|是|无|
|page|String|行为发生的页面|否|location.pathname的值|

addBehavior\(\)使用示例：

```
_bl.addBehavior({
  data:{name:'string',message:'sting'},
  page:'string'
})
```

[\[回到顶部\]](#sc_index)

## reportBehavior\(\)

调用reportBehavior\(\)接口即刻上报当前行为队列。

若不手动调用此接口，发生JS Error会自动触发上报当前行为队列，最大为100条，若超出100条，队列头的行为将被舍弃。

**说明：** 您需要在SDK配置中将behavior配置为true，才可调用此参数。

reportBehavior\(\)语法：

```
__bl.reportBehavior()
```

reportBehavior\(\)调用参数：无请求参数。

[\[回到顶部\]](#sc_index)

## performance\(\)

**说明：** 仅支持在Web端使用。

在页面onLoad之后调用performance\(\)接口来上报除默认性能指标外的自定义性能指标。

**说明：** 调用此方法的时间必须是在页面onLoad之后，否则会因尚未完成默认性能指标采集而导致调用无效。一次PV期间只能有效调用一次。

performance\(\)使用方法：

1.  将SDK配置项autoSendPerf设置为false，从而关闭自动上报性能指标，并等待手动触发上报。
2.  调用\_\_bl.performance\(Object\)方法来手动上报自定义指标，此过程中也会自动上报默认性能指标。

performance\(\)使用示例1（以CDN方式接入时）：

```
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …});
  }, 1000); //设置一定的延时，确保默认性能数据采集完成。
};
```

performance\(\)使用示例2（以npm包方式接入时）：

```
const BrowserLogger = require('alife-logger');
const __bl = BrowserLogger.singleton({pid:'站点唯一ID'});
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …});
  }, 1000); //设置一定的延时，确保默认性能数据采集完成。
};
```

**说明：** 自定义性能指标含义：

-   cfpt：自定义首次渲染时间
-   ctti：自定义首次可交互时间
-   t1 ~ t10：其他自定义性能指标（共计10个）

[\[回到顶部\]](#sc_index)

## setConfig\(\)

在SDK初始完成后调用setConfig\(\)接口来重新修改部分配置项，关于SDK配置项的详细信息，请参见[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)。

setConfig\(\)语法：

```
__bl.setConfig(next)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|next|Object|需要修改的配置项以及值|是|无|

setConfig\(\)使用示例：修改disableHook禁用API自动上报。

```
__bl.setConfig({
    disableHook: true
});            
```

[\[回到顶部\]](#sc_index)

## setPage\(\)

调用setPage\(\)接口来重新设置页面的page name（默认会触发重新上报PV）。此接口一般用于单页面应用，更多信息，请参见[SPA页面上报](/intl.zh-CN/前端监控/前端监控特殊使用场景/SPA页面上报.md)。

setPage\(\)语法：

```
__bl.setPage(page, sendPv)
```

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|page|String|新的page name|是|无|
|sendPv|Boolean|是否上报PV，默认会上报。|否|`true`|

setPage\(\)使用示例1：设置当前页面的page name为当前的URL hash，并重新上报PV。

```
__bl.setPage(location.hash);            
```

setPage\(\)使用示例2：仅设置当前页面的page为“homepage”，但不触发PV上报。

```
__bl.setPage('homepage', false);     
```

[\[回到顶部\]](#sc_index)

## 常见问题

问：如果调用\_\_bl.performance\(\)方法时不确定SDK是否已加载完成怎么办？

答：请参见[t152282.md\#section\_nsg\_w5u\_r05](/intl.zh-CN/前端监控/前端监控特殊使用场景/SPA页面上报.mdsection_nsg_w5u_r05)。

[\[回到顶部\]](#sc_index)

**相关文档**  


[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)

[SPA页面上报](/intl.zh-CN/前端监控/前端监控特殊使用场景/SPA页面上报.md)

