# Common parameters

This topic lists the common parameters of Application Real-Time Monitoring Service \(ARMS\) API operations and ARMS endpoints.

**Note:** The POP gateway provides services by using the Internet. If you cannot use the Internet, you cannot access the services.

## Common request parameters

|Parameter|Description|
|---------|-----------|
|region|The region of the API gateway. For information about supported regions, see [Endpoints](#section_m38_3x3_jky).|
|accessKeyId/accessKeySecret|-   If you use an Alibaba Cloud account or a RAM user to call an API operation, this parameter is the AccessKey pair of the account.
-   If you use a RAM role to call an API operation, this parameter is the AccessKey pair in the Security Token Service \(STS\) token that you obtained. For more information, see [Overview](/intl.en-US/Access control/Overview.md). |
|endpoint|The ID of the region. The region ID must be consistent with the region that is specified by the region parameter. Example: cn-hangzhou.|
|productName|The name of the product. Set the value to ARMS.|
|domain|The endpoint. Example: arms.\[region\].aliyuncs.com. For example, the endpoint of the China \(Hangzhou\) region is arms.cn-hangzhou.aliyuncs.com. For more information, see [Endpoints](#section_m38_3x3_jky).|

## Endpoints

To reduce network latency, we recommend that you specify the endpoint based on the region where you initiate API requests. The following table describes the endpoints of the ARMS API.

|Region|Endpoint|
|------|--------|
|China \(Hangzhou\)|arms.cn-hangzhou.aliyuncs.com|
|China \(Shanghai\)|arms.cn-shanghai.aliyuncs.com|
|China \(Qingdao\)|arms.cn-qingdao.aliyuncs.com|
|China \(Beijing\)|arms.cn-beijing.aliyuncs.com|
|China \(Shenzhen\)|arms.cn-shenzhen.aliyuncs.com|
|China \(Zhangjiakou\)|arms.cn-zhangjiakou.aliyuncs.com|
|China \(Hong Kong\)|arms.cn-hongkong.aliyuncs.com|
|Singapore \(Singapore\)|arms.ap-southeast-1.aliyuncs.com|

**Note:**

-   A maximum of 100 API requests can be initiated per second for a single IP address.
-   ARMS provides Internet endpoints. If your ECS instance does not have a public bandwidth package or a public IP address, you cannot initiate API requests by using tools such as Alibaba Cloud CLI or SDKs. For information about how to initiate requests from an ECS instance in a VPC that is not accessible to the Internet, see [Call API operations by using the internal network](/intl.en-US/API reference/Appendix/Call API operations by using the internal network.md).

**Related topics**  


[Overview](/intl.en-US/Access control/Overview.md)

