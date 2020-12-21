# 如何通过内网调用API

本文通过配置云解析PrivateZone，为无公网访问能力的专有网络VPC类型的ECS实例提供了通过阿里云内网调用API的方案。

由于ARMS提供的接入地址（Endpoint）为公网服务地址，当您的ECS实例没有分配公网带宽或者不存在公网IP地址时，则无法使用阿里云CLI或者SDK等工具发起API请求。此时，您可以为ECS实例所在地域下的专有网络VPC关联云解析PrivateZone，即可完成在阿里云内网调用API的目的。

## 使用说明

-   此方案仅适用于专有网络VPC类型的ECS实例所在的地域，不支持跨地域配置云解析PrivateZone。
-   建议您使用已部署了阿里云CLI或者SDK的自定义镜像创建ECS实例，避免实例在无公网访问的条件下无法加载相关依赖。
-   目前，支持云解析PrivateZone的ARMS接入地址（Endpoint）如下表所示，请确保您使用的Endpoint在列举范围内。

    |阿里云地域|地域ID|CNAME记录值|接入地址（Endpoint）|
    |-----|----|--------|--------------|
    |华东1（杭州）|cn-hangzhou|popunify-vpc.cn-hangzhou.aliyuncs.com|arms.cn-hangzhou.aliyuncs.com|
    |华东2（上海）|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|arms.cn-shanghai.aliyuncs.com|
    |华北1（青岛）|cn-qingdao|popunify-vpc.cn-qingdao.aliyuncs.com|arms.cn-qingdao.aliyuncs.com|
    |华北2（北京）|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|arms.cn-beijing.aliyuncs.com|
    |华南1（深圳）|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|arms.cn-shenzhen.aliyuncs.com|
    |华北3（张家口）|cn-zhangjiakou|popunify-vpc.cn-zhangjiakou.aliyuncs.com|arms.cn-zhangjiakou.aliyuncs.com|
    |中国（香港）|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|arms.cn-hongkong.aliyuncs.com|
    |新加坡|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|arms.ap-southeast-1.aliyuncs.com|


## 操作步骤

1.  登录[云解析DNS控制台](https://dns.console.aliyun.com/#/dns/domainList)。

2.  在左侧导航栏中，单击**PrivateZone**后，在**PrivateZone**页面单击**添加Zone**。

3.  在**添加PrivateZone**对话框中，完成以下设置后，单击**确定**。

    -   **Zone名称**：设置一个已支持云解析PrivateZone的ARMS接入地址，例如arms.cn-hangzhou.aliyuncs.com。
    -   **子域名递归解析代理**：选择该功能后，在VPC内查询Zone命名空间内未配置的子域名时，PrivateZone会代理公网递归解析，并将递归解析结果做为DNS查询响应，返回VPC。
    ![Add Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4674358061/p68391.png)

4.  在Zone列表找到已创建的PrivateZone，单击**操作**列的**解析设置**。

5.  在**解析设置**页面的**解析设置**页签，单击**添加记录**。

6.  在**添加记录**对话框中，完成以下设置后，单击**确定**。

    -   **记录类型**：选择**CNAME**。
    -   **主机记录**：填写为@，可以解析@.exmaple.com域名。
    -   **记录值**：设置为对应地域下的CNAME记录值，详情请参见[使用说明](#section_opq_9x8_52e)。
    -   **TTL值**：递归DNS缓存域名解析结果的时间，本示例选择了**1分钟**。
    ![Add Record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4674358061/p68396.png)

7.  返回**PrivateZone**页面，找到已创建的PrivateZone，单击**操作**列的**关联VPC**。

8.  在关联VPC对话框中，选择与PrivateZone相同的地域，并勾选ECS实例所在的专有网络VPC（可多选），单击**确定**。

    ![Bind VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4674358061/p68406.png)


## 执行结果

为专有网络VPC关联了云解析PrivateZone后，您可以通过远程连接登录实例，在ECS实例内部测试是否能访问对应地域的接入地址，详情请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

以下以arms.cn-hangzhou.aliyuncs.com为例，使用ping功能测试数据包收发状况。

```
ping arms.cn-hangzhou.aliyuncs.com
```

当出现类似以下显示结果时，表示可以访问对应地域的接入地址。

![Ping Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4674358061/p68407.png)

