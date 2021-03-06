# ARMS Open API 概述 {#concept_42924_zh .concept}

OpenAPI 底层通过 HTTP 接口提供服务，您调用 OpenAPI 的 SDK，发出 HTTP 请求到应用网关 POP，再由 POP 将请求转发给 ARMS 的后端服务去执行。

您将参数封装到每个请求中，每个请求即对应一个方法。执行的结果放在 response 中。

**说明：** 因为 POP 网关是面对公网环境提供服务的，因此使用 OpenAPI 的前提是能够访问公网服务，否则会提示服务无法连接。

## POP 参数说明 {#section_xv3_gby_gfb .section}

|参数|说明|
|--|--|
|region|API 网关所在区域，目前支持华东 1、华东 2、华北 1、华北 2、华南 1|
|accessKeyId／accessKeySecret| -   如果您以主账号或 RAM 子账号调用 OpenAPI，则此处为主账号或 RAM 子账号的 accessKeyId/accessKeySecret；

-   如果您以 RAM 用户角色调用 OpenAPI，则此处为您获取的 STS 安全令牌中的accessKeyId/accessKeySecret。详情请参见[访问控制概述](../../../../../intl.zh-CN/访问控制/访问控制概述.md#)。


 |
|endpoint|接入点名称与 region 保持一致，例如 cn-hangzhou|
|productName|Open API 的产品名称，直接写 ARMS 即可|
|domain|目前为 arms.\[region\].aliyuncs.com，例如 arms.cn-hangzhou.aliyuncs.com|

## 地域说明 { .section}

|地域名称|RegionId|
|----|--------|
|华东 1（杭州）|cn-hangzhou|
|华东 2（上海）|cn-shanghai|
|华北 1（青岛）|cn-qingdao|
|华北 2（北京）|cn-beijing|
|华南 1（深圳）|cn-shenzhen|

**说明：** Open API 对单 IP 调用次数限制为 100 次/秒。

## 更多信息 { .section}

-   [访问控制概述](../../../../../intl.zh-CN/访问控制/访问控制概述.md#)

