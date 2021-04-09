# Exception diagnotics

This topic shows you how to view the exception diagnotics of an application.

The application is monitored by Application Real-Time Monitoring Service \(ARMS\). For more information, see [Overview](/intl.en-US/Application Monitoring/Quick start/Overview.md).

## Go to the Exceptions Diagnosis page

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, Select **Application monitoring** \> **Applications**.

3.  In the top navigation bar of the MNS console, select the region where your cluster is deployed.

4.  Log on to the **Applications**Page, click the application name.

5.  In the left-side navigation pane, choose **Application Diagnosis** \> **Exceptions Diagnosis**.

6.  On the right side of the Exceptions Diagnosis page, specify a time range and click the exception that you want to view.

    ![Exception Diagnosis](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p254560.png)


## Number of exceptions

In the **Exceptions** section, you can view the trend of the number of times the exception has been thrown during the specified time range.

![Number of exceptions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p254569.png)

1.  In the **Exceptions** section, perform the following operations as required:

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.

## List of APIs that throw the exception

This list displays the information about the APIs that throw the exception, including the API name, the exception summary, the number of times that the exception has been thrown, and the proportion of the exception within each API.

![APIs that throw the exception](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p254570.png)

1.  In the list, perform the following operations as required:

    -   In the **Exception Name** column, click the name of the exception to view the exception details.

        ![Exception name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p255351.png)

        -   On the **Error Information** tab of the **Exception Details** panel, you can view the information about the exception stack.

            ![Error Information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p254577.png)

        -   On the **Related Trace** tab of the **Exception Details** panel, you can view the information about the exceptions that were captured within the selected API.

            ![Related Trace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6554397161/p254578.png)

            You can click a trace ID in the **TraceId** column to view the trace of the exception.

            For more information about how to analyze traces, see [Analyze traces](/intl.en-US/Application Monitoring/Console functions/Trace query.md).

    -   In the **Interface** column, click the name of an API to view the information about API calls.

        For more information about API calls, see [API monitoring](/intl.en-US/Application Monitoring/Console functions/API monitoring.md).

    -   Move the cursor over the statistics chart to view the statistics.
    -   Select a period of time to view the statistics for the specified period.

