# 以 npm 方式安装探针 {#concept_66404_zh .concept}

要使用 ARMS 前端监控监控 Web 应用，必须先以 CDN 或 npm 方式安装探针。本文介绍如何以 npm 方式为 Web 应用安装 ARMS 前端监控探针。

## 安装 {#section_rm2_zct_s2b .section}

在 npm 仓库中安装 `alife-logger`。

``` {#codeblock_xyc_bvk_45z}
npm install alife-logger --save
```

## 使用 {#section_fm4_bdt_s2b .section}

**初始化**

SDK 以 `BrowerLogger.singleton` 方式初始化。

``` {#codeblock_3h2_13g_s54}
const BrowerLogger = require('alife-logger');
// BrowserLogger.singleton(conf) conf传入config配置
const __bl = BrowerLogger.singleton({
    pid: 'your-project-id',
    imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', // 设定日志上传地址,新加坡部署可选`https://arms-retcode-sg.aliyuncs.com/r.png?`
    // 其他config配置
});
```

使用 npm 方式接入 ARMS 前端监控时，Web 端 SDK 会自动生成 UID 来统计 UV 等信息。自动生成的 UID 可以用来区分用户的标识，但不具有业务属性，若您想自定义 UID，请在上述代码中加入以下内容：

``` {#codeblock_5e4_pb4_4hz}
uid: 'xxx', // 该值用于区分用户的标识，根据业务设置
```

例如：

``` {#codeblock_lxm_z63_8ny}
const BrowserLogger = require('alife-logger');
// BrowserLogger.singleton(conf) conf传入config配置
const __bl = BrowserLogger.singleton({
    pid: 'your-project-id',
    uid: 'xxx', // 该值用于区分用户的标识，根据业务设置
    imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', // 设定日志上传地址,新加坡部署可选`https://arms-retcode-sg.aliyuncs.com/r.png?`
    // 其他config配置
});
```

**API 说明**

**@static singleton\(\) 获取单例对象**

**说明：** 该方法只适用于 npm 引入。

调用参数说明：`BrowerLogger.singleton(config,prePipe)`

静态方法，返回一个单例对象，传入的 config、prePipe 只在第一次调用时生效，此后调用只返回已经生成的实例。

|参数|类型|描述|是否必须|默认值|
|--|--|--|----|---|
|config|Object|站点配置，其他配置查看 \#config 配置项|是|-|
|prePipe|Array|预上报内容|否|-|

此方法可以用于在应用入口初始化 SDK，也可以在每次调用时获取实例。

**其他上报 API**

通过 `BrowerLogger.singleton` 获取实例。

``` {#codeblock_49c_eyp_lig}
const __bl = BrowerLogger.singleton();
```

关于 `__bl` 的其他 API 使用方式，请参考 [API 使用指南](intl.zh-CN/前端监控/高级选项/API 使用指南.md#)。

**Config 配置**

Config 配置与 CDN 引入配置相同。请参考[前端监控 SDK 配置项](intl.zh-CN/前端监控/高级选项/前端监控 SDK 配置项.md#)。

**预上报**

场景：在调用 `BrowserLogger.singleton()` 之前执行的部分逻辑需要上报一些数据。

``` {#codeblock_75o_0gv_dev}
const BrowerLogger = require('alife-logger');
// 与 CDN 的 Pipe 结构一致
const pipe = [
    // 将当前页面的 HTML 也作为一个 API 上报
    ['api', '/index.html', true, performance.now, 'SUCCESS'],
    // SDK 初始化完成后即开启 SPA 自动解析
    ['setConfig', {enableSPA: true}]
];
const __bl = BrowserLogger.singleton({pid:'站点唯一ID'},pipe);
```

