# Health inspection

The health inspection feature can be used to periodically test the connectivity of your monitored services. This feature allows you to know the health status of the monitored services and detect and handle exceptions at the earliest opportunity.

The services that you want to monitor are connected to Prometheus Monitoring. For more information, see [Get started with Prometheus Service]().

## Go to the Prometheus Monitoring page

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  In the top navigation bar, select a region.

4.  On the **Prometheus Monitoring** page, click the name of a Kubernetes cluster.

5.  In the left-side navigation pane, click **Health inspection**.


## Create a health inspection task

You can create a health inspection task for a specified service.

1.  In the upper-right corner of the **Health inspection** page, click **Create inspection**.

2.  In the **Create inspection** dialog box, set the parameters, click **Link test** to test the connectivity, and then click **OK**.

    ![Create a health inspection task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8548342161/p232683.png)

    |Parameter|Description|
    |---------|-----------|
    |Checkpoint|The checkpoint of the health inspection task. Enter an IP address or a domain name. For example, you can set the value to 11.113.2.1 or www.aliyun.com.|
    |Inspection Type|The type of the health inspection task.    -   HTTP
    -   Ping
    -   HTTPS
    -   TCP |
    |Frequency|The interval at which the health inspection task is run. Valid values:    -   Every 10s
    -   Every 20s
    -   Every 60s
    -   Every 120s |


## Create a health inspection task for an Alibaba Cloud service

You can import the data of an Alibaba Cloud service that is collected by Prometheus Monitoring to create a health inspection task.

1.  In the upper-right corner of the **Health inspection** page, click **Cloud Service Inspection**.

2.  In the **Cloud Service Inspection** wizard, perform the following steps:

    1.  Select an Alibaba Cloud service whose data you want to import and click **Next**.

        **Note:** Prometheus Monitoring allows you to import the data of ApsaraDB for Redis and ApsaraDB RDS.

        ![Health inspection task for an Alibaba Cloud service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8548342161/p232697.png)

    2.  Select the data that you want to import and click **OK**.

        ![Health inspection task for an Alibaba Cloud service 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8548342161/p232701.png)


## Create a health inspection task for ACK

You can import the data of Container Service for Kubernetes \(ACK\) that is collected by Prometheus Monitoring to create a health inspection task.

1.  In the upper-right corner of the **Health inspection** page, click **ACK Inspection**.

2.  In the **Create ACK Inspection** dialog box, select the ACK data that you want to import and click **OK**.


## Modify a health inspection task

You can modify the parameter settings of a health inspection task.

1.  On the **Inspection** tab, find the health inspection task that you want to modify and click **Editing** in the **Actions** column.

2.  In the **Edit inspection** dialog box, modify the parameters, click **Link test** to test the connectivity, and then click **OK**.

    ![Modify a health inspection task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8548342161/p232713.png)

    For more information about the health inspection parameters, see [Table 1](#table_ql8_aia_3ms).


## Delete a health inspection task

You can delete health inspection tasks that you do not need.

1.  On the **Inspection** tab, you can perform the following operations:

    -   Delete a single health inspection task
        1.  In the **Actions** column of the health inspection task that you want to delete, click **Delete**.
        2.  In the message that appears, click **OK**.
    -   Delete multiple health inspection task at the same time

        Select the health inspection tasks that you want to delete and click **Batch Delete**.


