# Associate trace IDs with business logs

You can associate trace IDs with the business logs of an application. In this way, when an error occurs to the application, you can access the business logs associated with trace IDs to find out and troubleshoot the error.

The Application Real-Time Monitoring Service \(ARMS\) agent is upgraded to version 2.6.1.2 or later. For more information, see [FAQ about updating the ARMS agent for Java applications](/intl.en-US/Application monitoring/FAQ about updating the ARMS agent for Java applications.md).

In ARMS, trace IDs can be associated with business logs of an application based on the Mapped Diagnostic Context \(MDC\) mechanism. The Log4j, Log4j 2, and Logback mainstream log frameworks are supported.

## Associate trace IDs with business logs

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region. On the Applications page, click the name of the application.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Custom Configuration tab.

4.  On the Custom Configuration tab, turn on **Link Business Logs with TraceId** in the **Business Log Linking Settings** section.

    ![sc_am_log_correlation](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7919658061/p94135.png)

    **Note:**

    -   If Link Business Logs with TraceId is turned on, trace IDs are automatically generated in the business logs.
5.  Add `%X{EagleEye-TraceID}` to the pattern property of the business log layout. The following figure shows how to add this configuration for the Logback component.

    **Note:** For information about how to obtain \{EagleEye-TraceID\} from the business code, see [ARMS SDK](/intl.en-US/Application monitoring/References/ARMS SDK.md).

    ![dg_am__layout_pattern](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8381468061/p94145.png)

6.  Restart the application.

    If trace IDs are displayed in the business logs of the application, the business logs are associated with the trace IDs, as shown in the following figure.

    ![dg_am_log_traceid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8381468061/p94151.png)


