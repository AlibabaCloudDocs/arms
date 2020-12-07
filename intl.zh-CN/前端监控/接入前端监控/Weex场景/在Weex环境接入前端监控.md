# 在Weex环境接入前端监控

本文介绍如何在Weex环境中接入ARMS前端监控。

## 导入npm包

如需在Weex环境中使用ARMS前端监控，则首先需要在项目中执行以下命令导入alife-logger npm包，以使用专门的WeexLogger模块来上报日志。

```
npm install alife-logger --save
```

## 初始化

在/utils目录下创建monitor.js文件，并按照以下示例代码完成SDK初始化。

**说明：** 在Weex应用入口调用singleton\(props\)静态方法获取实例时，需要在传入的props中设定相关配置，请参见：

-   [通用API：@static singleton\(\)](#section_mof_zn6_n9l)
-   [通用API：setPage\(\)](#section_a9k_j3s_i38)
-   [通用API：setConfig\(\)](#section_t5p_nqr_kn6)

```
// 在monitor.js文件中增加以下内容。
import WeexLogger from 'alife-logger/weex';

const fetch = weex.requireModule('stream').fetch;
const serialize = (data) = >{
    data = data || {};
    var arr = [];
    for (var k in data) {
        if (Object.prototype.hasOwnProperty.call(data, k) && data[k] !== undefined) {
            arr.push(k + '=' + encodeURIComponent(data[k]).replace(/\(/g, '%28').replace(/\)/g, '%29'));
        }
    }
    return arr.join('&');
}

// 初始化SDK。
const wxLogger = WeexLogger.singleton({
    pid: 'your-project-id',
    uid: 'zhangsan',
    // 设置uid，用于生成UV报告。
    page: 'Lazada | Home',
    // 设置初始页面名称。SDK将在初始化完成后发送PV日志。
    imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?',
    // 设定日志上传地址。如需部署至新加坡地域，则改为'https://arms-retcode-sg.aliyuncs.com/r.png?'。
    // 设置GET上报方法，示例如下：
    sendRequest: (data, imgUrl) = >{
        const url = imgUrl + serialize(data);
        fetch({
            method: 'GET',
            url
        });
    },
    // 设置POST上报方法，示例如下：
    postRequest: (data, imgUrl) = >{
        fetch({
            method: 'POST',
            type: 'json',
            url: imgUrl,
            body: JSON.stringify(data)
        });
    }
});

export
default wxLogger;
```

## 上报

通过实例调用相应的上报方法进行上报。

```
// in some biz module
import wxLogger from '/utils/monitor';
wxLogger.api('/search.do', true, 233, 'SUCCESS');
```

## 通用API：@static singleton\(\)

@static singleton\(\)为静态方法，作用是返回一个单例对象。props只在第一次调用时生效，用法如下表所示。

此方法可用于在应用入口初始化SDK，请参见[初始化](#initialization)。

|属性|类型|描述|是否必需|默认值|
|--|--|--|----|---|
|pid|String|站点ID|是|无|
|page|String|初始化的Page Name|否|无|
|uid|String|用户ID|是|无|
|imgUrl|String|日志上传地址，以英文问号（?）结尾。|否|无|

## 通用API：setPage\(\)

setPage\(\)的作用是设置当前页面的Page Name，并且默认上报一次PV日志。

```
import wxLogger from '/utils/monitor';
// ...
wxLogger.setPage(nextPage);
```

|参数|类型|描述|是否必需|默认值|
|--|--|--|----|---|
|nextPage|String|Page Name|是|无|

## 通用API：setConfig\(\)

setConfig\(\)的作用是在SDK初始化完成后修改部分配置项，具体配置与singleton\(\)方法相同。配置项详情，请参见[setConfig\(\)](/intl.zh-CN/前端监控/API参考.md)。

```
import wxLogger from '/utils/monitor';
// ...
wxLogger.setConfig(config);
```

|参数|类型|描述|是否必需|默认值|
|--|--|--|----|---|
|config|Object|需要修改的配置项以及值。|是|无|
|uid|String|用户ID，用于统计UV。|是|Storage设置|

## 日志上报API

请参见[API参考](/intl.zh-CN/前端监控/API参考.md)中的日志上报接口。

## 通用SDK配置项

ARMS前端监控提供一系列SDK配置项，让您能够通过设置参数来满足额外需求。以下是适用于本文场景的通用配置项。

|参数|类型|描述|是否必选|默认值|
|--|--|--|----|---|
|pid|String|项目唯一ID，由ARMS在创建站点时自动生成。|是|无|
|uid|String|用户ID，用于标识访问用户，可手动配置，用于根据用户ID检索。如果不配置，则由SDK自动生成且每半年更新一次。|是|无|
|tag|String|传入的标记，每条日志都会携带该标记。|否|无|
|release|String|应用版本号。建议您配置，便于查看不同版本的上报信息。|否|`undefined`|
|environment|String|环境字段，取值为：prod、gray、pre、daily和local，其中： -   prod表示线上环境。
-   gray表示灰度环境。
-   pre表示预发环境。
-   daily表示日常环境。
-   local表示本地环境。

|否|`prod`|
|sample|Integer|日志采样配置，值为`1`、`10`或`100`。性能和成功API日志按照`1/sample`的比例采样。|否|`1`|

ARMS前端监控还提供了更多SDK配置项，可满足进一步的需求。更多信息，请参见[SDK参考](/intl.zh-CN/前端监控/SDK参考.md)。

