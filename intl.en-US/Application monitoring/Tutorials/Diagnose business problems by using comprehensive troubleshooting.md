# Diagnose business problems by using comprehensive troubleshooting

Comprehensive troubleshooting is used to quickly locate the problem link by using the business primary key. Comprehensive troubleshooting must be used together with the custom monitoring feature. This topic describes how to use comprehensive troubleshooting.

## Prerequisites

-   An application monitoring task is created. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md).

-   The following dependencies are added to the pom.xml file:

    ```
    <dependency>
    <groupId>com.alibaba.arms.apm</groupId>
    <artifactId>arms-sdk</artifactId>
    <version>1.7.1</version>
    </dependency>
    ```

    The Maven repository address is `https://oss.sonatype.org`.

    **Note:** If you cannot retrieve the pom.xml file, download [arms-sdk-1.7.1.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.1.jar).


## Retrieve TraceId and RpcId

After the preceding prerequisites are met, run the following commands to obtain the TraceId and RpcId:

```
Span span = Tracer.builder().getSpan();
String traceId = span.getTraceId();
String rpcId = span.getRpcId();
```

## Retrieve logs

After TraceId and RpcId are obtained, you can retrieve and export business logs as needed. The following sample business log contains TraceId and RpcId. By default, this log is exported to /Home/admin/logs/example.log. However, you can also export it to other channels such as Log Service and Message Queue.

```
2018-07-12 11:37:40|1e057c4015313666599651005d1201|0|username=xiao,age=22,action=login
2018-07-12 11:37:40|1e057c4015313666599651005d1201|0|username=xiao,age=22,action=search
2018-07-12 11:37:40|1e057c4015313666599651005d1201|0|username=xiao,age=22,action=cart
```

Each of the preceding business logs represents a user trajectory.

## Configure a comprehensive troubleshooting event set

The preceding sample business logs are used as the data source. Create a custom monitoring task and split logs according to the following scheme. For more information, see [Create a custom monitoring job](/intl.en-US/Quick start/Create a custom monitoring job.md).

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0107358061/p42297.png)

Create a comprehensive troubleshooting event set and configure the event set as shown in the following figure. or more information, see [Create a comprehensive troubleshooting event set]().

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0107358061/p42298.png)

-   Business Primary Key: The field that is used to search for business events. In this topic, action and username are used in the example.

-   Time Field: Select the business time instead of the system time.

-   TraceID: Set the TraceId.

-   RpcID: Set the RpcId.


Activate custom monitoring after you configure the event set.

## Use cases of comprehensive troubleshooting

In this example, the business log shows the user trajectory. The corresponding application is a shopping website. If the user kevin.yang complains that an order failed after 14:20 on July 12, 2018, you can identify the causes for the failure by using the following two methods.

-   Method 1: Query traces

    1.  In the left-side navigation pane, choose **Application Monitoring** \> **Traces and Events**, and access the Traces and Events tab of the Instances page.
    2.  Enter the date range as the **Date** value on the tab. In the **Parameter Name** drop-down list, select **Business Primary Key**. Enter the value \(in this case Username: kevin.yang\) of the business primary key in the **Parameter Value** field on the right. Then click **Query**. All traces within the specified time range are displayed in the search results.

    3.  In the search results, click the TraceId of the abnormal trace, and then click the **Business Trace** tab. All business events of this TraceId appear. Locate the causes for the exception.

-   Method 2: Query comprehensive troubleshooting events

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Invocation Trace Query**, and click the Trace Query tab of the Instances page.
2.  In the left-side navigation pane, click **Multi-Dimensional Query**, and click the Query Holographic Troubleshooting Events tab.

3.  Enter a date range in the **Date** field. In the drop-down list **Holographic Troubleshooting Event Set**, select the previously configured event set, and click **Query**. All traces within the specified time range are displayed in the search results.

4.  In the search results, click **Trace Query**, and then click the Business Trace tab. All business events of this TraceId appear, and causes for the exception are located.


## References

-   [Create a comprehensive troubleshooting event set]()

