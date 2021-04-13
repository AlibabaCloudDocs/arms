# Call the ARMS API over the internal network

This topic describes how to configure Alibaba Cloud DNS PrivateZone \(PrivateZone\). This way, an Elastic Compute Service \(ECS\) instance in a virtual private cloud \(VPC\) that has no access to the Internet can call the Application Real-Time Monitoring Service \(ARMS\) API over the Alibaba Cloud internal network.

ARMS provides public endpoints. If your ECS instance does not have a public bandwidth or a public IP address, you cannot make API requests by using tools such as Alibaba Cloud CLI or SDK. Alibaba Cloud provides PrivateZone to ensure that your ECS instance can send API requests over the Alibaba Cloud internal network. You can associate PrivateZone with the VPC in the region where your ECS instance is located.

## Usage notes

-   You can configure PrivateZone only for regions that contain VPC-connected ECS instances. You cannot configure PrivateZone across regions.
-   We recommend that you use custom images that have Alibaba Cloud CLI or SDK deployed to create ECS instances. Otherwise, the ECS instances cannot load related dependencies without Internet access.
-   The following table describes the ARMS endpoints that support PrivateZone. Make sure that you use an endpoint listed in the table.

    |Alibaba Cloud region|Region ID|CNAME record|Endpoint|
    |--------------------|---------|------------|--------|
    |China \(Hangzhou\)|cn-hangzhou|popunify-vpc.cn-hangzhou.aliyuncs.com|arms.cn-hangzhou.aliyuncs.com|
    |China \(Shanghai\)|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|arms.cn-shanghai.aliyuncs.com|
    |China \(Qingdao\)|cn-qingdao|popunify-vpc.cn-qingdao.aliyuncs.com|arms.cn-qingdao.aliyuncs.com|
    |China \(Beijing\)|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|arms.cn-beijing.aliyuncs.com|
    |China \(Shenzhen\)|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|arms.cn-shenzhen.aliyuncs.com|
    |China \(Zhangjiakou\)|cn-zhangjiakou|popunify-vpc.cn-zhangjiakou.aliyuncs.com|arms.cn-zhangjiakou.aliyuncs.com|
    |China \(Hong Kong\)|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|arms.cn-hongkong.aliyuncs.com|
    |Singapore \(Singapore\)|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|arms.ap-southeast-1.aliyuncs.com|


## Procedure

1.  Log on to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/#/dns/domainList).

2.  In the left-side navigation pane, click **PrivateZone**. On the **PrivateZone** page, click **Add Zone**.

3.  In the **Add PrivateZone** dialog box, set the following parameters and click **OK**.

    -   **Zone Name**: Enter an ARMS endpoint that supports PrivateZone. In this example, enter arms.cn-hangzhou.aliyuncs.com.
    -   **Subdomain recursive resolution proxy**: If you select this option, when you query the subdomain names that are not configured in the zone namespace in the VPC, PrivateZone recursively resolves the subdomain names on the Internet. PrivateZone uses the recursive resolution result as the DNS response to your query and returns this response to the VPC.
    ![Add Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68391.png)

4.  On the PrivateZone page, find the created private zone in the zone list and click **Configure** in the **Actions** column.

5.  On the **Resolution Settings** page, click the **Resolution Settings** tab. On the Resolution Settings tab, click **Add Record**.

6.  In the **Add Record** dialog box, set the following parameters and click **OK**.

    -   **Record Type**: Select **CNAME**.
    -   **Resource Records**: Enter @ to resolve the @.example.com domain name.
    -   **Record Value**: Enter the CNAME record of the corresponding region. For more information, see [Usage notes](#section_opq_9x8_52e).
    -   **TTL value**: the time period during which recursive DNS caches the domain name resolution results. In this example, select **1 minute**.
    ![Add Record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68396.png)

7.  On the **PrivateZone** page, find the created private zone and click **Bind VPC** in the **Actions** column.

8.  In the Bind VPC panel, select the same region as the created private zone, select the VPC where your ECS instance is located, and then click **Confirm**. You can select multiple VPCs.

    ![Bind VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1669758061/p68406.png)


## Verify the result

After you associate the VPC with the created private zone, you can log on to your ECS instance to check whether this ECS instance can access the ARMS endpoint of the corresponding region. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

arms.cn-hangzhou.aliyuncs.com is used in this example. Run the ping command to test the status of packet sending and receiving.

```
ping arms.cn-hangzhou.aliyuncs.com
```

If a result similar to the following content appears, your ECS instance can access the ARMS endpoint of the corresponding region.

![Ping Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68407.png)

