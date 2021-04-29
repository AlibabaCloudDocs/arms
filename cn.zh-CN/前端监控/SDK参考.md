# SDK参考

ARMS前端监控提供一系列SDK配置项，让您能够通过设置参数来满足额外需求，例如忽略指定URL、API、JS错误的上报、通过过滤URL中的非关键字符使页面聚类、通过随机采样上报来减小上报量并降低负载等。

## 本页索引

[pid](#sc_pid) \| [uid](#sc_uid) \| [tag](#sc_tag) \| [page](#sc_page) \| [setUsername](#sc_setusername) \| [enableSPA](#sc_enablespa) \| [parseHash](#sc_parsehash) \| [disableHook](#sc_disablehook) \| [ignoreUrlCase](#sc_ignoreurlcase) \| [urlHelper](#sc_urlhelper) \| [apiHelper](#sc_apihelper) \| [parseResponse](#sc_parseresponse) \| [ignore](#sc_ignore) \| [disabled](#sc_disabled) \| [sample](#sc_sample) \| [sendResource](#sc_sendresource) \| [useFmp](#sc_usefmp) \| [enableLinkTrace](#sc_enablelinktrace) \| [release](#sc_release) \| [environment](#sc_environment) \| [behavior](#sc_behavior) \| [c1\\c2\\c3](#sc_custom) \| [autoSendPerf](#sc_autosendperf)

## 如何使用前端监控SDK配置项

可通过以下两种方式使用前端监控SDK配置项：

-   向页面插入BI探针时在config中添加额外参数。

    例如，以下示例代码的config中，除了默认的pid参数外，还添加了用于单页面应用（Single Page Application）场景的enableSPA参数。

    ```
    <script>
    !(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxxxxx",enableSPA:true};
    with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
    })(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
    </script>                    
    ```

-   页面初始化完成后，在前端JS代码中调用setConfig方法来修改配置项。

    `__bl.setConfig(next)`调用参数说明：

    |参数|类型|描述|是否必选|默认值|
    |--|--|--|----|---|
    |next|Object|需要修改的配置项以及值|是|无|

    示例：修改disableHook禁用API自动上报。

    ```
    __bl.setConfig({
        disableHook: true
    });            
    ```


## pid

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|pid|String|项目唯一ID，由ARMS在创建站点时自动生成。|是|无|

[\[回到顶部\]](#sc_index)

## uid

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|uid|String|用户ID，用于标识访问用户，可手动配置，用于根据用户ID检索。如果不配置，则由SDK随机自动生成且每半年更新一次。|-   Weex场景：必需
-   其他场景：非必需

|-   Weex场景：无
-   其他场景：由SDK自动生成 |

示例：调用setConfig方法修改SDK配置项。

```
__bl.setConfig({
    uid: 12345
});        
```

[\[回到顶部\]](#sc_index)

## tag

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|tag|String|传入的标记，每条日志都会携带该标记。|否|无|

[\[回到顶部\]](#sc_index)

## page

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|page|String|页面名称。|否|默认取当前页面URL的关键部分：`host + pathname`。|

[\[回到顶部\]](#sc_index)

## setUsername

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|setUsername|Function|用于设置一个方法，该方法需要返回类型为String的用户名称。|否|无|

本配置项用于设置一个方法，该方法需要返回类型为String的用户名称。配置后可以根据用户名称进行全链路追踪（会话追踪）、查询用户会话轨迹，便于排查问题。

**说明：** 若页面加载初期暂时无法获取用户名，则可设置返回Null，但不要设置返回一个临时用户名。因为SDK发送日志时会再次调用setUsername方法获取用户名，如果之前设置了返回临时用户名，则会一直沿用最初设置的用户名，不再重新获取。

示例：调用setConfig方法修改SDK配置项。

```
__bl.setConfig({
    setUsername: function () {
        return "username_xxx";
    }
});            
```

[\[回到顶部\]](#sc_index)

## enableSPA

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|enableSPA|Boolean|监听页面的hashchange事件并重新上报PV，适用于单页面应用场景。|否（仅Web场景支持）|`false`|

[\[回到顶部\]](#sc_index)

## parseHash

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|parseHash|Function|与enableSPA搭配使用。|否|见下文|

单页面应用场景中（参见[SPA页面上报](/cn.zh-CN/前端监控/前端监控特殊使用场景/SPA页面上报.md)），在enableSPA设为`true`的前提下，页面触发hashchange事件时，parseHash参数用于将URL Hash解析为Page字段。

**默认值**

其默认值由一个简单的字符串处理方法获得：

```
function (hash) {
    var page = hash ? hash.replace(/^#/, '').replace(/\?.*$/, '') : '';
    return page || '[index]';
}           
```

此项一般情况下不需要修改。如果需要在上报时使用自定义的页面名，或者URL的Hash比较复杂，则需要修改此配置项。例如：

```
// 定义页面Hash和Page的映射关系。
var PAGE_MAP = {
    '/': '首页',
    '/contact': '联系我们',
    '/list': '数据列表',
    // ...
};
// 页面load后调用SDK方法。
window.addEventListener('load', function (e) {
    // 调用setConfig方法修改SDK配置项。
    __bl.setConfig({
        parseHash: function (hash) {
            key = hash.replace(/\?.*$/, '');
            return PAGE_MAP[key] || '未知页面';
        }
    });
});
```

[\[回到顶部\]](#sc_index)

## disableHook

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|disableHook|Boolean|禁用AJAX请求监听。|否|`false`：默认会监听并用于API调用成功率上报。|

[\[回到顶部\]](#sc_index)

## ignoreUrlCase

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|ignoreUrlCase|Boolean|忽略Page URL大小写。|否|`true`：默认忽略。|

[\[回到顶部\]](#sc_index)

## urlHelper

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|urlHelper|\*|代替旧参数ignoreUrlPath，用于配置URL过滤规则。|否|见下文|

当页面URL类似于`http://xxx.com/projects/123456`（projects后面的数字是项目ID）时，如果将`xxx.com/projects/123456`作为page上报，会导致在数据查看时页面无法聚成一类。这种情况下，为了使同类页面聚类，可以使用urlHelper参数过滤掉非关键字符，例如此例中的项目ID。

**说明：**

-   用于URL过滤规则的旧参数ignoreUrlPath现已废弃，请使用新参数urlHelper。若继续使用旧参数且不使用新参数，配置仍将生效。若同时使用新旧参数，则新参数的配置生效。
-   此配置项只在自动获取页面URL作为Page时才会生效。如果手动调用setPage或setConfig方法（参考[API参考](/cn.zh-CN/前端监控/API参考.md)）修改过Page，或者如果enableSPA已设为`true`，则此设置项无效。

**默认值**

此配置项的默认值是以下数组，一般情况下不需要修改。

```
[
    // 将所有Path中的数字变成*。
    {rule: /\/([a-z\-_]+)?\d{2,20}/g, target: '/$1**'},
    // 去掉URL末尾的'/'。
    /\/$/
]                    
```

此设置项的默认值会过滤掉`xxxx/123456`后面的数字，例如`xxxx/00001`和`xxxx/00002`都会变成`xxxx/**`。

**值类型**

urlHelper的值可以是以下类型：

-   `String`或`RegExp`（正则表达式）：将匹配到的字符串去掉。
-   `Object<rule, target>`：对象包含两个Key（rule和target）作为JS字符串的replace方法的入参。使用方法参见JS相关教程中的String::replace方法。
-   `Function`：将原字符串作为入参执行方法，将执行结果作为Page。
-   `Array`：用于设置多条规则，每条规则都可以是上述类型之一。

[\[回到顶部\]](#sc_index)

## apiHelper

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|apiHelper|\*|代替旧参数ignoreApiPath，用于配置API过滤规则。|否|见下文|

用于在自动上报API时过滤接口URL中的非关键字符，用法及含义同[urlHelper](#sc_urlhelper)。

**说明：** 用于API过滤规则的旧参数ignoreApiPath现已废弃，请使用新参数apiHelper。若继续使用旧参数且不使用新参数，配置仍将生效。若同时使用新旧参数，则新参数的配置生效，旧参数的配置不生效。

**默认值**

默认值是一个对象，一般情况下不需要修改：

```
{rule: /(\w+)\/\d{2,}/g, target: '$1'}                    
```

此设置项的默认值会过滤掉接口URL中类似`xxxx/123456`后面的数字。

如果需要在API中上报`?`后面的参数，例如：`https://arms.console.aliyun.com/apm?pid=fr6fbgbeot`中的pid参数，需要按照以下方法手动上报API数据：

-   使用ignore方法，关闭自动上报。具体操作，请参见[ignore](#sc_ignore)。
-   使用api\(\)自行上报API数据。具体操作，请参见[api\(\)](/cn.zh-CN/前端监控/API参考.md)。

[\[回到顶部\]](#sc_index)

## parseResponse

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|parseResponse|Function|用于解析自动上报API时返回的数据。|否|见下文|

该配置项用于解析自动上报API时返回的数据。

**默认值**

该配置项的默认值为：

```
function (res) {
    if (!res || typeof res !== 'object') return {};
    var code = res.code;
    var msg = res.msg || res.message || res.subMsg || res.errorMsg || res.ret || res.errorResponse || '';
    if (typeof msg === 'object') {
        code = code || msg.code;
        msg = msg.msg || msg.message || msg.info || msg.ret || JSON.stringify(msg);
    }
    return {msg: msg, code: code, success: true};
}                    
```

以上代码会解析返回的数据，尝试提取出`msg`和`code`。对于一般应用来说，此设置项不需要修改。如果默认值无法满足业务需求，则可以重新设置。

[\[回到顶部\]](#sc_index)

## ignore

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|ignore|Object|忽略指定URL/API/JS错误。符合规则的日志将被忽略且不会被上报，包含子配置项ignoreUrls、ignoreApis、ignoreErrors和ignoreResErrors。|否|见下文|

ignore的值是一个对象，对象中包含4个属性：ignoreUrls、ignoreApis、ignoreErrors和ignoreResErrors。可单独设置其中的1个或多个属性。

**默认值**

该配置性的默认值为：

```
ignore: {
        ignoreUrls: [],
        ignoreApis: [],
        ignoreErrors: [],
        ignoreResErrors: []
    },                    
```

ignoreUrls

ignoreUrls表示忽略某些URL，符合规则的URL下的日志都不会被上报。值可以是`String`、`RegExp`、`Function`或者以上三种类型组成的数组。示例：

```
__bl.setConfig({
                ignore: {
                    ignoreUrls: [
                    'http://host1/',  // 字符串
                    /.+?host2.+/,     // 正则表达式
                    function(str) {   // 方法
                        if (str && str.indexOf('host3') >= 0) {
                            return true;   // 不上报
                        }
                        return false;      // 上报
                    }]
                }
            });                    
```

ignoreApis

ignoreApis表示忽略某些API，符合规则的API将不会被监控。值可以是`String`、`RegExp`、`Function`或者以上三种类型组成的数组。示例：

```
__bl.setConfig({
                ignore: {
                    ignoreApis: [
                    'api1','api2','api3', // 字符串
                    /^random/,  // 正则表达式
                    function(str) { // 方法
                        if (str && str.indexOf('api3') >= 0) return true;   // 不上报
                        return false;   // 上报
                    }]
                }
            });                    
```

ignoreErrors

ignoreErrors表示忽略某些JS错误，符合规则的JS错误不会被上报。值可以是`String`、`RegExp`、`Function`或者以上三种类型组成的数组。示例：

```
__bl.setConfig({
                ignore: {
                    ignoreErrors: [
                    'test error', // 字符串
                    /^Script error\.?$/, // 正则表达式
                    function(str) { // 方法
                        if (str && str.indexOf('Unkown error') >= 0) return true;   // 不上报
                        return false;   // 上报
                    }]
                }
            });            
```

ignoreResErrors

ignoreResErrors表示忽略指定的资源错误，符合规则的资源错误不会被上报。值可以是`String`、`RegExp`、`Function`或者以上三种类型组成的数组。示例：

```
__bl.setConfig({
                ignore: {
                    ignoreResErrors: [
                    'http://xx/picture.jpg', // 字符串
                    /jpg$/, // 正则表达式
                    function(str) { // 方法
                        if (str && str.indexOf('xx.jpg') >= 0) return true;   // 不上报
                        return false;   // 上报
                    }]
                }
            });
```

[\[回到顶部\]](#sc_index)

## disabled

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|disabled|Boolean|禁用日志上报功能。|否|`false`|

[\[回到顶部\]](#sc_index)

## sample

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|sample|Integer|日志采样配置，值为1~100的整数。对性能日志和成功API日志按照`1/sample`的比例采样，关于性能日志和成功API日志的指标说明，请参见[统计指标说明](/cn.zh-CN/前端监控/统计指标说明.md)。|否|`1`|

sample配置项作用：

-   减小API的数据上报量（降低部分费用），更精确的方案建议使用ignore参数过滤掉某些不需要监控的API数据，更多信息，请参考[ignore](#sc_ignore)。
-   降低采集数据的性能开销。

sample配置项说明：

-   为了减小上报量和降低负载，该配置项会对性能和成功API日志进行随机采样上报，后台处理日志时会根据对应的采样配置进行还原，因此不会影响JS错误率和失败API率等指标的计算。但是会导致在查询API详情或者相关数据明细的时候，无法保证百分之百可以查看明细。

-   采样值`sample`默认为`1`，值可以是1~100的整数，对应的采样率为`1/sample`，例如：`1`表示100% 采样，`10`表示10% 采样，`100`表示1% 采样。


**警告：** 由于是随机采样，如果原上报量较小，该配置项可能会造成较大的统计结果误差，建议仅日均PV在100万以上的站点使用该配置项。

[\[回到顶部\]](#sc_index)

## sendResource

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|sendResource|Boolean|上报页面静态资源。|否|`false`|

如果sendResource配置为`true`，则页面load事件触发时会上报当前页面加载的静态资源信息。如果发现页面加载较慢，可以在会话追踪页面查看页面加载的静态资源瀑布图，判断页面加载较慢的具体原因。

sendResource示例代码：

```
<script>
!(function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxxxxx",sendResource:true};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>            
```

**说明：** 由于是在页面load事件触发时判断，所以请在config中配置sendResource（如以上示例所示），不要使用setConfig的方式，因为这种方式可能在页面load事件完成后才会触发，从而使该配置项会无效。

[\[回到顶部\]](#sc_index)

## useFmp

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|useFmp|Boolean|采集首屏FMP（First Meaningful Paint，首次有效渲染）数据。|否|`false`|

[\[回到顶部\]](#sc_index)

## enableLinkTrace

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|enableLinkTrace|Boolean|进行前后端链路追踪，请参见[t152278.md\#](/cn.zh-CN/前端监控/使用教程/使用前后端链路追踪诊断API错误原因.md)。|否（仅Web场景、支付宝小程序、微信小程序、钉钉小程序支持）|`false`|

[\[回到顶部\]](#sc_index)

## release

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|release|String|应用版本号。建议您配置，便于查看不同版本的上报信息。|否|`undefined`|

[\[回到顶部\]](#sc_index)

## environment

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|environment|String|环境字段，取值为：prod、gray、pre、daily和local，其中： -   prod表示线上环境。
-   gray表示灰度环境。
-   pre表示预发环境。
-   daily表示日常环境。
-   local表示本地环境。

|否|`prod`|

[\[回到顶部\]](#sc_index)

## behavior

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|behavior|Boolean|是否为了便于排查错误而记录报错的用户行为。|否（仅Web场景和小程序场景支持）|Browser默认为`true`，小程序默认为`false`。|

[\[回到顶部\]](#sc_index)

## autoSendPerf

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|autoSendPerf|Boolean|是否允许自动发送性能日志。|否|`true`|

[\[回到顶部\]](#sc_index)

## c1\\c2\\c3

除了以上列出的配置项，您可能还需要更多的附加信息辅助处理业务问题，因此ARMS SDK提供了3个可自定义字段的配置项，配置后字段内容会包含在每一条上报的日志中。

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|c1|String|业务自定义字段，每条日志都会携带该标记。|否|无|
|c2|String|业务自定义字段，每条日志都会携带该标记。|否|无|
|c3|String|业务自定义字段，每条日志都会携带该标记。|否|无|

[\[回到顶部\]](#sc_index)

**相关文档**  


[API参考](/cn.zh-CN/前端监控/API参考.md)

[SPA页面上报](/cn.zh-CN/前端监控/前端监控特殊使用场景/SPA页面上报.md)

[数据预上报](/cn.zh-CN/前端监控/前端监控特殊使用场景/数据预上报.md)

