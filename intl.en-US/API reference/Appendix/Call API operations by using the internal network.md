# Call API operations by using the internal network

This topic describes how to configure Alibaba Cloud DNS PrivateZone \(PrivateZone\). In this way, an Elastic Compute Service \(ECS\) instance in a Virtual Private Cloud \(VPC\) that has no access to the Internet can initiate API requests by using the Alibaba Cloud internal network.

Application Real-Time Monitoring Service \(ARMS\) provides public network endpoints. However, if your ECS instance does not have a public bandwidth package or a public IP address, this ECS instance cannot initiate an API request by using tools such as Alibaba Cloud Command-line Interface \(CLI\) or corresponding SDKs. Alibaba Cloud provides PrivateZone to ensure that your ECS instance can send API requests over the Alibaba Cloud internal network. You can associate PrivateZone with the VPC in the region to which your ECS instance belongs.

## Instructions

-   You can configure PrivateZone only for regions that contain VPC-type ECS instances. You cannot configure PrivateZone across multiple regions.
-   We recommend that you use a custom image that is deployed with Alibaba Cloud CLI or SDK to create an ECS instance. Otherwise, the ECS instance cannot load related dependencies without public network access.
-   The following table describes the endpoints that support PrivateZone. Make sure that you use an endpoint listed in the table.

    |Alibaba Cloud region|Region ID|CNAME record|Public network endpoint|
    |--------------------|---------|------------|-----------------------|
    |China \(Hangzhou\)|cn-hangzhou-b|popunify-vpc.cn-hangzhou.aliyuncs.com|arms.cn-hangzhou.aliyuncs.com|
    |China \(Shanghai\)|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|arms.cn-shanghai.aliyuncs.com|
    |China \(Qingdao\)|cn-qingdao|popunify-vpc.cn-qingdao.aliyuncs.com|arms.cn-qingdao.aliyuncs.com|
    |China \(Beijing\)|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|arms.cn-beijing.aliyuncs.com|
    |China \(Shenzhen\)|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|arms.cn-shenzhen.aliyuncs.com|
    |China \(Zhangjiakou\)|cn-zhangjiakou|popunify-vpc.cn-zhangjiakou.aliyuncs.com|arms.cn-zhangjiakou.aliyuncs.com|
    |China \(Hong Kong\)|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|arms.cn-hongkong.aliyuncs.com|
    |Singapore \(Singapore\)|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|arms.ap-southeast-1.aliyuncs.com|


## Procedure

1.  Log on to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/#/dns/domainList).

2.  In the left-side navigation pane, click **PrivateZone**. On the **PrivateZone** page, click **Add Zone** on the All Zones tab.

3.  In the **Add PrivateZone** dialog box, set the following two parameters as required, and then click **OK**.

    -   **Zone Name**: Enter an endpoint that is provided by ARMS and supports PrivateZone. In this example, enter arms.cn-hangzhou.aliyuncs.com.
    -   **Subdomain recursive resolution proxy**: If you select this option, when you query the subdomain names that are not configured in the zone namespace in the VPC, PrivateZone will recursively resolve the subdomain names on the Internet, and use the recursive resolution result as the DNS response to your query. Then PrivateZone returns this response to the VPC.
    ![Add Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68391.png)

4.  On the PrivateZone page, click the All Zones tab. On the All Zones tab, find the created private zone in the zone list, and click **Configure** in the **Actions** column.

5.  On the **Resolution Settings** page, click the **Resolution Settings** tab. On the Resolution Settings tab, click **Add Record**.

6.  In the **Add Record** dialog box, set the following parameters, and then click **OK**.

    -   **Record Type**: Select **CNAME** from the drop-down list.
    -   **Resource Records**: Enter @ to resolve the @.example.com domain name.
    -   **Record Value**: Enter the CNAME record of the corresponding region. For more information, see [Instructions](#section_opq_9x8_52e).
    -   **TTL Value**: The time-to-live \(TTL\) value. In this example, select **1 minute\(s\)**.
    ![Add Record](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68396.png)

7.  On the **PrivateZone** page, find the created private zone, and click **Bind VPC** in the **Actions** column.

8.  In the Bind VPC dialog box, select the same region as the created private zone, select the VPC where your ECS instance is located, and then click **OK**. You can select multiple VPCs.

    ![Bind VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1669758061/p68406.png)


## Results

After you associate the VPC with the created private zone, you can log on to your ECS instance to check whether this ECS instance can access the endpoint of the corresponding region. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

Take arms.cn-hangzhou.aliyuncs.com as an example. Run the ping command to test the status of packet sending and receiving.

```
ping arms.cn-hangzhou.aliyuncs.com
```

![Ping Private Zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1609158061/p68407.png)

