# QueryMetric（前端监控）

调用QueryMetric接口查询前端监控的相关监控指标。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ARMS&api=QueryMetric&type=RPC&version=2019-08-08)

## 描述

QueryMetric接口可用于查询应用监控和前端监控的相关监控指标。本文以查询前端监控的相关指标为例。

|API名称|Request|Response|
|-----|-------|--------|
|QueryMetric|QueryMetricRequest|QueryMetricResponse|

## 请求参数

请求参数包含公共参数和业务参数。

**公共参数**

公共请求参数请参见[公共参数](/cn.zh-CN/API 参考/公共参数.md)。

**业务参数**

阿里云将用户的所有请求参数封装在一个Request中，返回一个Response。

|名称|类型|设置方法|是否必选|示例值|描述|
|--|--|----|----|---|--|
|StartTime|Long|setStartTime|是|1595319532000|查询数据的起始时间。|
|EndTime|Long|setEndTime|是|1596183532000|查询数据的截止时间。|
|Metric|String|setMetric|是|webstat.index|需查询的指标，不可自定义输入，详情请参见[可查询的前端监控指标](#section_jtc_apg_9ii)。|
|Measures|List\[String\]|setMesures|是|\["pv","uv"\]|指标对应的测量数据，详情请参见[可查询的前端监控指标](#section_jtc_apg_9ii)。最多可添加5个。|
|Dimensions|List\[String\]|setDimensionss|否|\["detector\_browser","detector\_device"\]|指标对应的维度，详情请参见[可查询的前端监控指标](#section_jtc_apg_9ii)。最多可添加5个。|
|Filters|List\[Filter\]|setFilters|是|\[\{key:pid,value:xxx@74xxx\},\{key:regionId,value:cn-hangzhou\}\]|筛选条件组合，必须添加pid和regionId条件，pid获取方式请参见[如何获取应用pid](#sc_pid)。|
|IntervalInSec|Integer|setIntervalInSec|否|100,000|数据片的时间间隔，单位为毫秒，最小值为60,000。**说明：** 如需不限制时间范围，则将该参数设为2147483647。 |
|OrderBy|String|setOrderBy|否|count|排序依据，可设为任一测量数据。|
|Limit|Integer|setLimit|否|100|自定义的返回结果数量限制。**说明：** 因为POP网关的限制，超出10,000条的数据将被去除。 |
|Order|String|setOrder|否|ASC|排序标准： -   ASC：升序
-   DESC：降序 |
|SecurityToken|String|setSecurityToken|否|atc19s\*\*\*\*\*\*\*|STS SecurityToken，采用RAM用户角色模式时需要设置该字段。详情请参见[借助RAM角色实现跨云账号访问资源](/cn.zh-CN/访问控制/借助RAM角色实现跨云账号访问资源.md)。|

**Filters复合字段说明**

|字段名称|字段类型|设置方法|字段含义|取值|
|----|----|----|----|--|
|Key|String|setKey|维度名称|-   pid（必选）
-   regionId（必选）
-   environment（可选） |
|Value|String|setValue|维度值|-   pid的示例值：xxx@74xxx
-   regionId的示例值：cn-hangzhou
-   environment的取值：
    -   prod：表示线上环境
    -   gray：表示灰度环境
    -   pre：表示预发环境
    -   daily：表示日常环境
    -   local：表示本地环境 |

**说明：** 前端监控所有的指标查询中必须在Filters中添加pid和regionId条件。

## 如何获取前端应用pid

登录[ARMS控制台](https://arms.console.aliyun.com/#/home)，在控制台左侧导航栏单击**前端监控**，然后在**前端监控**页面单击目标前端应用名称，以进入该前端应用的总览页面。

此时浏览器地址栏中的URL即包含前端应用的pid，格式为`pid=xxx`。由于浏览器进行了编码，前端应用需要对pid稍作修改。例如，如果URL中包含的pid为`xxx%4074xxx`，则需要将`%40`替换为`@`，即：`xxx@74xxx`。

## 返回参数

返回值为JSON串形式，可通过QueryMetricResponse.getdata\(\)获取。

|字段名称|字段含义|
|----|----|
|data|数据点|

## 可查询的前端监控指标

您可以使用QueryMetric接口查询前端监控的以下指标。

**说明：** 已知具体的查询条件时，应将值传入Filters参数中，用于限定查询结果的范围。如果不知道具体的查询条件，可以将下表中的维度传入dimensions参数，从而获得该维度所有可能值的列表。

|指标（Metric）|描述|维度（Dimensions）|测量数据（Measures）|
|----------|--|--------------|--------------|
|webstat.api|API成功率|-   api（API请求地址，不带参数）
-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   release（版本号）
-   sr（屏幕分辨率）

|-   count（请求次数）
-   rate（API成功率）
-   avg\_time（平均耗时） |
|webstat.api.detail|API详情|-   api（API请求地址，不带参数）
-   ct（网络制式）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   domain（域名）
-   ip\_country\_id（中国省市ID）
-   ip\_isp（运营商）
-   ip\_region\_id（国家ID或区域ID）
-   msg（返回信息）
-   page（页面地址）
-   sr（屏幕分辨率）

|-   count（请求次数）
-   fail\_count（失败次数）
-   fail\_time（失败耗时）
-   fail\_uv（失败影响用户数）
-   success\_count（成功次数）
-   success\_rate（成功率）
-   success\_time（成功耗时） |
|webstat.apicost|API成功耗时|-   api（API请求地址，不带参数）
-   code（返回状态码）
-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   release（版本号）
-   sr（屏幕分辨率）

|-   count（成功次数）
-   avg\_time（成功耗时均值） |
|webstat.apifailtime|API失败耗时|-   api（API请求地址，不带参数）
-   code（返回状态码）
-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   release（版本号）
-   sr（屏幕分辨率）

|-   count（错误次数）
-   avg\_time（失败耗时均值） |
|webstat.apimsg|API消息聚类|-   code（返回状态码）
-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   msg（错误信息）
-   release（版本号）
-   sr（屏幕分辨率）
-   success（1表示请求成功，0表示请求失败）

|count（请求次数） |
|webstat.avg|自定义统计：均值统计|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   key（自定义Key）
-   sr（屏幕分辨率）

|-   count（总次数）
-   pv（页面浏览量）
-   uv
-   avg\_val（平均值） |
|webstat.errcate|错误聚类排行|-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   msg（错误信息）
-   page（页面地址）
-   release（版本号）
-   sr（屏幕分辨率）

|count（错误次数） |
|webstat.index|总览（访问量）|-   ct（网络制式）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_isp（运营商）
-   ip\_region\_id（国家ID或区域ID）
-   page（页面地址）
-   sr（屏幕分辨率）

|-   pv（页面浏览量）
-   uv（独立访客） |
|webstat.msg.top|页面高频错误|-   msg（错误信息）
-   page（页面地址）

|-   count（错误次数）
-   error\_uv（影响用户数）
-   影响用户率（影响用户数÷总UV） |
|webstat.perf.bucket|对应ARMS前端监控控制台的**访问速度**页面上的性能样本分层图。|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   page（页面地址）
-   sr（屏幕分辨率）

|-   cfpt（自定义首屏）
-   ctti（自定义首次可交互）
-   dns（DNS查询耗时）
-   dom（DOM解析耗时）
-   fmp（首屏时间）
-   fpt（首次渲染时间）
-   load（页面完全加载时间）
-   ready（DOM Ready时间）
-   res（资源加载耗时）
-   ssl（SSL安全连接耗时）
-   t1~t10（自定义性能指标）
-   tcp（TCP连接耗时）
-   trans（内容传输耗时）
-   ttfb（请求响应耗时）
-   tti（首次可交互时间） |
|webstat.perf.distribution|对应ARMS前端监控控制台的**访问速度**页面上的性能分层图。|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   page（页面地址）
-   sr（屏幕分辨率）

|-   cfpt（自定义首屏）
-   ctti（自定义首次可交互）
-   dns（DNS查询耗时）
-   dom（DOM解析耗时）
-   fmp（首屏时间）
-   fpt（首次渲染时间）
-   load（页面完全加载时间）
-   ready（DOM Ready时间）
-   res（资源加载耗时）
-   ssl（SSL安全连接耗时）
-   t1~t10（自定义性能指标）
-   tcp（TCP连接耗时）
-   trans（内容传输耗时）
-   ttfb（请求响应耗时）
-   tti（首次可交互时间） |
|webstat.resource|资源错误排行|-   ct（网络制式）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_isp（运营商）
-   ip\_region\_id（国家ID或区域ID）
-   node\_name（错误类型）
-   page（页面地址）
-   sr（屏幕分辨率）
-   src（资源信息）

|count（资源错误数）|
|webstat.resource|对应ARMS前端监控控制台的**总览**页面的资源弹层。|-   ct（网络制式）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_isp（运营商）
-   ip\_region\_id（国家ID或区域ID）
-   node\_name（错误类型）
-   page（页面地址）
-   sr（屏幕分辨率）
-   src（资源信息）

|count（错误次数）|
|webstat.satisfy|满意度|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   page（页面地址）
-   sr（屏幕分辨率）

|-   bad（不满意：fpt\>8000）
-   good（满意：fpt<2000）
-   neutral（可容忍：fpt\>2000且fpt<8000）
-   satisfy（满意指数） |
|webstat.session|慢加载追踪|无|-   browser\_version（浏览器版本）
-   browser（浏览器）
-   date（开始时间）
-   dom（DOM解析耗时）
-   ip\_country\_id（中国省市ID）
-   ip\_country（中国省市）
-   ip\_region\_id（国家ID或区域ID）
-   ip\_region（国家或区域）
-   load（页面完全加载）
-   page（页面地址）
-   sid（会话ID） |
|webstat.speed|访问速度|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   release（版本号）
-   sr（屏幕分辨率）
-   page（页面地址）
-   environment（环境）

|-   avg\_cfpt（自定义首屏）
-   count（样本量）
-   avg\_ctti（自定义首次可交互）
-   avg\_dns（DNS查询耗时）
-   avg\_dom（DOM解析耗时）
-   avg\_fmp（首屏时间）
-   avg\_fpt（首次渲染时间）
-   avg\_load（页面完全加载时间）
-   avg\_ready（DOM Ready时间）
-   avg\_res（资源加载耗时）
-   avg\_ssl（SSL安全连接耗时）
-   avg\_t1~t10（自定义性能指标）
-   avg\_tcp（TCP连接耗时）
-   avg\_trans（内容传输耗时）
-   avg\_ttfb（请求响应耗时）
-   avg\_tti（首次可交互时间） |
|webstat.stable|错误率排行|-   detector\_app\_version（客户端版本）
-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   release（版本号）
-   sr（屏幕分辨率）

|-   count（样本量）
-   error\_pv（错误样本量）
-   rate（JS错误率） |
|webstat.sum|自定义统计：求和统计|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   key（自定义key）
-   sr（屏幕分辨率）

|-   count（总次数）
-   pv（页面浏览量）
-   sum\_val（总和）
-   uv（独立访客） |
|webstat.url|访问的URL|-   detector\_browser（浏览器）
-   detector\_device（设备）
-   detector\_os（操作系统）
-   ip\_country\_id（中国省市ID）
-   ip\_region\_id（国家ID或区域ID）
-   sr（屏幕分辨率）
-   uid
-   username（用户名）

|-   pv（页面浏览量）
-   uv（独立访客） |

## 示例代码

使用QueryMetric接口查询前端监控总览页面的PV与UV的示例代码如下：

## 常见问题

-   调用时为什么会出现RAM的权限问题？

    这可能是由于该RAM角色没有权限，您可以为用户添加权限，详情请参见[借助RAM角色实现跨云账号访问资源](/cn.zh-CN/访问控制/借助RAM角色实现跨云账号访问资源.md)。

-   怎么拉取列表数据（不考虑时间粒度）？

    将intervalInSec设置为2147483647。

-   为什么返回的数据值都为0？

    -   请检查时间间隔是否设置过小，intervalInSec需要大于或等于60,000。
    -   请检查regionId是否设置正确，该regionId是根据日志接收的服务端划分的地域，而不是用户所在的地域，您可以根据项目的上报日志地址来区分regionId：
        -   华东1（杭州）地域前端监控上报日志地址：`https://arms-retcode.aliyuncs.com/r.png?`。
        -   新加坡（新加坡）地域前端监控上报日志地址：`https://arms-ap-southeast-1.console.aliyun.com/r.png?`。
        -   美国（硅谷）地域前端监控上报日志地址：`http://arms-us-west-1.console.aliyun.com/r.png?`。
-   在调用模拟器或代码接口时为什么会报错？

    -   请检查regionId是否已填写，filters中是否已添加pid。
    -   查看对应指标的measures或dimensions是否正确，详情请参见[可查询的前端监控指标](#section_jtc_apg_9ii)。
-   报错信息以及对应解决方案

    -   **Metric查询错误，请联系管理员。**
        -   请检查Metric字段是否正确。
        -   请检查measures或dimensions是否正确。
        -   请检查filters中是否已添加pid。
    -   **InvalidIntervalInSec**

        请检查intervalInSec是否超过最大值（2147483647）。

    -   **MissingMeasures**

        请检查measures是否已填写。

    -   **NonsequenceParameter.Dimensions**
        -   请检查dimensions是否已填写正确。
        -   请检查模拟器dimensions是否有多余的空格。
    -   **ServiceUnavailable**

        请检查regionId是否正确。

    -   **前端监控地域不合法**

        请检查regionId是否设置正确，该regionId是根据日志接收的服务端划分的地域，而不是用户所在的地域，您可以根据项目的上报日志地址来区分regionId：

        -   华东1（杭州）地域前端监控上报日志地址：`https://arms-retcode.aliyuncs.com/r.png?`。
        -   新加坡（新加坡）地域前端监控上报日志地址：`https://arms-ap-southeast-1.console.aliyun.com/r.png?`。
        -   美国（硅谷）地域前端监控上报日志地址： `http://arms-us-west-1.console.aliyun.com/r.png?`。
-   为什么数据集中会缺失一些 measures或dimensions参数？

    因为最多可设置5个measures和dimensions，如果超过5个，将导致参数无法返回。

-   为什么一些指标的总数在聚合后明显少于未聚合时？例如：webstat.index聚合后求和的pv总数比未聚合时得到的pv总数少。

    因为POP网关的限制，超出10,000条的数据将被去除，所以当聚合造成数据量超过限制时，返回的数据量比实际的量小，因此指标求和的总数会明显减少。您需要将每次请求后返回的数据量控制在10,000条以内，以获得准确的数据。


