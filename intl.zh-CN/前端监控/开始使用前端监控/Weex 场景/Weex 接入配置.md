# Weex 接入配置 {#concept_65674_zh .concept}

本文介绍了 weex 环境中云前端监控的接入配置。

## 导入 npm 包 {#section_frz_n11_ok2 .section}

在 weex 环境中，使用专门的 WeexLogger 模块来上报日志，接入时需要在项目中导入 `alife-logger` npm 包。

``` {#codeblock_yf4_hm0_cd3 .language-bash}
npm install alife-logger --save
```

## 初始化 {#initialization .section}

在 weex 应用入口调用 `singleton(props)` 静态方法获取实例，需要在传入的 `props` 中设定相关配置，详情参见[通用 API](#sc_general_api)。

``` {#codeblock_siv_ggm_2am .language-js}
// in app.js
import WeexLogger from 'alife-logger/weex';

const wxLogger = WeexLogger.singleton({
    pid: 'your-project-id',
    uid: 'zhangsan', // Login uid, for UV report
    page: 'Lazada | Home', // Initial page name, if passed, SDK will send a PV log after Initialization completed
    imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?' // 设定日志上传地址,新加坡部署可选`https://arms-retcode-sg.aliyuncs.com/r.png?`
});
```

## 上报 {#section_erc_ax8_i13 .section}

通过实例调用相应的上报方法进行上报。

``` {#codeblock_zoc_svj_87l .language-js}
// in some biz module
import WeexLogger from 'alife-logger/weex';

wxLogger.api('/search.do', true, 233, 'SUCCESS');
```

## 通用 API {#sc_general_api .section}

## @static singleton\(\) 获取单例对象 {#section_mof_zn6_n9l .section}

静态方法，返回一个单例对象。`props` 用法如下（只在第一次调用时生效）。

调用参数说明：`WeexLogger.singleton(props)`

|属性|类型|描述|是否必须|默认值|
|--|--|--|----|---|
|pid|String|站点 ID|是|-|
|page|String|初始化的 Page Name|否|-|
|uid|String|用户 ID|是|-|
|imgUrl|String|日志上传地址，以“?”结尾|否|-|

此方法可用于在应用入口初始化 SDK，示例参见[初始化](#initialization)。

## setPage\(\) 设置当前页面的 Page Name {#section_a9k_j3s_i38 .section}

设置 Page Name，并且上报一次 PV 日志（默认）。

调用参数说明：

``` {#codeblock_bhj_yuw_qs0 .language-js}
const wxLogger = WeexLogger.singleton();
// ...
wxLogger.setPage(nextPage);
			
```

|参数|类型|描述|是否必须|默认值|
|--|--|--|----|---|
|nextPage|String|Page Name|是|-|

## setConfig\(\) 修改配置项 {#section_t5p_nqr_kn6 .section}

用于在 SDK 初始化完成后修改部分配置项，具体配置同 `singleton()` 方法。

调用参数说明：

``` {#codeblock_fyf_omm_972 .language-js}
const wxLogger = WeexLogger.singleton();
// ...
wxLogger.setConfig(next);
			
```

|参数|类型|描述|是否必须|默认值|
|--|--|--|----|---|
|next|Object|需要修改的配置项以及值|是|-|

## 日志上报 API {#section_flf_7nq_39w .section}

请参见 [API 使用指南](intl.zh-CN/前端监控/高级选项/API 使用指南.md#)的“日志上报接口”。

