# 以npm方式接入前端监控

要使用ARMS前端监控子产品监控Web应用，必须先以CDN或npm方式安装探针。本文介绍如何以npm方式为Web应用安装ARMS前端监控探针。

## 安装

在npm仓库中安装`alife-logger`。

```
npm install alife-logger --save
```

## 初始化

SDK以`BrowserLogger.singleton`方式初始化。

```
const BrowserLogger = require('alife-logger');
                // BrowserLogger.singleton(conf) conf传入config配置。
                const __bl = BrowserLogger.singleton({
                pid: 'your-project-id',
                // 设定日志上传地址：
                // 部署新加坡地域可设为`https://arms-retcode-sg.aliyuncs.com/r.png?`。
                // 部署美西地域可设为`http://arms-us-west-1.console.aliyun.com/r.png?`。
                imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', 
                // 其他config配置。
                });
```

使用npm方式接入ARMS前端监控时，Web端SDK会自动生成UID来统计UV等信息。自动生成的UID可以用来区分用户的标识，但不具有业务属性，如需自定义UID，请在上述代码中加入以下内容：

```
uid: 'xxx', // 该值用于区分用户的标识，根据业务设置。
```

示例：

```
const BrowserLogger = require('alife-logger');
                // BrowserLogger.singleton(conf) conf传入config配置。
                const __bl = BrowserLogger.singleton({
                    pid: 'your-project-id',
                        // 设定日志上传地址：
                        // 部署新加坡地域可设为`https://arms-retcode-sg.aliyuncs.com/r.png?`。
                        // 部署美西地域可设为`http://arms-us-west-1.console.aliyun.com/r.png?`。
                    uid: 'xxx', // 该值用于区分用户的标识，根据业务设置。
                        imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', 
                    // 其他config配置。
                });
```

## API说明



**说明：** 该方法只适用于npm引入。

调用参数说明：`BrowserLogger.singleton(config,prePipe)`

静态方法，返回一个单例对象，传入的config、prePipe只在第一次调用时生效，此后调用只返回已经生成的实例。

|参数|类型|描述|是否必须|默认值|
|--|--|--|----|---|
|config|Object|站点配置，其他配置查看config配置项，请参见[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)。|是|无|
|prePipe|Array|预上报内容|否|无|

此方法可以用于在应用入口初始化SDK，也可以在每次调用时获取实例。

通过`BrowserLogger.singleton`获取实例。

```
const __bl = BrowserLogger.singleton();
```

关于`__bl`的其他API使用方式，请参见[API参考](/intl.zh-CN/前端监控/API参考.md)。

Config配置与CDN引入配置相同。请参见[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)。

如果在调用`BrowserLogger.singleton()`之前执行的部分逻辑需要上报一些数据，则需要使用数据预上报。具体操作，请参见[数据预上报](/intl.zh-CN/前端监控/前端监控特殊使用场景/数据预上报.md)。

```
const BrowserLogger = require('alife-logger');
                // 与CDN的Pipe结构一致。
                const pipe = [
                // 将当前页面的HTML也作为一个API上报。
                ['api', '/index.html', true, performance.now, 'SUCCESS'], //相当于__bl.api(api, success, time, code, msg)。
                // SDK初始化完成后即开启SPA自动解析。
                ['setConfig', {enableSPA: true}]
                ];
                const __bl = BrowserLogger.singleton({pid:'站点唯一ID'},pipe);
```

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
|sample|Integer|日志采样配置，值为`1`、`10`或`100`。性能和成功API日志按照`1/sample`的比例采样。|否|`1`|
|behavior|Boolean|是否为了便于排查错误而记录报错的用户行为。|否|`true`|
|enableSPA|Boolean|监听页面的hashchange事件并重新上报PV，适用于单页面应用场景。|否|`false`|
|enableLinkTrace|Boolean|进行前后端链路追踪，请参见[t152278.md\#](/intl.zh-CN/前端监控/使用教程/使用前后端链路追踪诊断API错误原因.md)。|否|`false`|

ARMS前端监控还提供了更多SDK配置项，可满足进一步的需求。更多信息，请参见[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)。

**相关文档**  


[前端监控接入概述](/intl.zh-CN/前端监控/接入前端监控/前端监控接入概述.md)

[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)

[以CDN方式接入前端监控](/intl.zh-CN/前端监控/接入前端监控/Web场景/以CDN方式接入前端监控.md)

[在Weex环境接入前端监控](/intl.zh-CN/前端监控/接入前端监控/Weex场景/在Weex环境接入前端监控.md)

