# Common parameters

This topic lists the common parameters for Application Real-Time Monitoring Service \(ARMS\) API operations and supported regions.

**Note:** The pctowap open platform \(POP\) gateway provides services through the public network. Therefore, to use the API operations, you must be able to access the public network. Otherwise, a service connection failure occurs.

## Common request parameters

|Parameter|Description|
|---------|-----------|
|region|The region of the API gateway. For more information about supported regions, see [Regions supported by ARMS](#section_m38_3x3_jky).|
|accessKeyId/accessKeySecret|-   If you use an Alibaba Cloud primary account or a RAM user to call an API operation, this parameter is the accessKeyId/accessKeySecret of the Alibaba Cloud primary account or the RAM user.
-   If you use a RAM role to call an API operation, this parameter is the accessKeyId/accessKeySecret in the Security Token Service \(STS\) token that you obtained. For more information, see [Access control overview](https://www.alibabacloud.com/help/doc-detail/74783.htm). |
|endpoint|The endpoint name must be consistent with the region, for example "cn-hangzhou".|
|productName|The product name. Set this value to ARMS.|
|domain|Set this value to arms.\[region\].aliyuncs.com. For example, the region China \(Hangzhou\) is arms.cn-hangzhou.aliyuncs.com.|

## Regions supported by ARMS

|Region|ID|
|------|--|
|China \(Hangzhou\)|cn-hangzhou|
|China \(Shanghai\)|cn-shanghai|
|China \(Qingdao\)|cn-qingdao|
|China \(Beijing\)|cn-beijing|
|China \(Shenzhen\)|cn-shenzhen|
|China \(Zhangjiakou\)|cn-zhangjiakou|
|China \(Hong Kong\)|cn-hongkong|
|Singapore|ap-southeast-1|

**Note:** A single IP address can call API operations up to 100 times per second.

