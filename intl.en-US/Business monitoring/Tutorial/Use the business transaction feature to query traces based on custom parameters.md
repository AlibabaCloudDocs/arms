---
keyword: [business transaction, custom parameter, trace]
---

# Use the business transaction feature to query traces based on custom parameters

The built-in query fields supported by the ARMS trace query feature are not business-related and cannot meet the query requirements of specific business scenarios. You can use the business transaction feature to configure extraction rules for the custom parameters of your application. Then, the business transaction feature can obtain the corresponding parameters and add them to traces. You can query the traces based on the custom parameters.

You have access to the ARMS business transaction feature. For more information, see [Overview](/intl.en-US/Application monitoring/Overview.md).

**Note:** Make sure that you have upgraded your agent to version 2.7.1 or later.

ARMS provides the trace query feature and supports query criteria such as the trace ID, interface name, IP address, and HTTP status code. However, these query criteria are not business-related and you cannot use this feature to query fields such as user ID or order ID that contain business information. You can use the business transaction feature to fix the issue.

After you access the business transaction feature, you only need to configure extraction rules for custom parameters and this feature can use agents to obtain the parameters and add them to traces. Then, you can easily and precisely locate traces based on the custom parameters.

Compared with the holographic troubleshooting feature and the grouping rules feature, the custom parameter extraction feature has more advantages. The following table summarizes the differences among the three features.

|Monitoring method|Access cost|Timeliness|Flexibility|
|-----------------|-----------|----------|-----------|
|Business transaction \(custom parameter extraction\)|Low. The system collects and reports data based on agent information.|Real-time. Data is aggregated and calculated in the background and displayed on a timely basis.|High. You can configure multiple extraction rules and all business data is reported.|
|Business transaction \(grouping rules\)|Low. The system collects and reports data based on agent information.|Real-time. Data is aggregated and calculated in the background and displayed on a timely basis.|Limited. You can configure only one grouping rule for each application and only the first 10 queried entries of business data are displayed.|
|Holographic troubleshooting|High. You must modify the application by correlating business information with the trace in logs.|Real-time.|Low. You must change the logs for the business information to be analyzed to display.|

## Configure extraction rules for custom parameters

Before you can query traces based on custom parameters, you must configure extraction rules for the custom parameters of your application.

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications** and select a region from the drop-down list in the upper-left corner.

3.  On the **Applications** page, click **Settings** in the right-side **Actions** column corresponding to the application.

4.  On the **Application Settings** page, click the **Custom parameters** tab and click **Add custom parameter** in the upper-right corner.

5.  In the **Add custom parameter** dialog box, configure the following parameters and click **OK**.

    |Parameter|Description|Required|Example|
    |---------|-----------|--------|-------|
    |Rule name|The name of the extraction rule.|Yes|Custom parameter to be extracted|
    |Interface type|Only HTTP is supported.|Yes|HTTP portal|
    |Parameter extraction rules|For an HTTP portal, you can select Parameter, Cookie, Method, or Header from the drop-down list. You can configure multiple extraction rules.|Yes|If you need to extract brand and account data from the `curl "http://{domain}/api/buy?brand=SIEMENS" -H "account: 123456"` interface, add the following extraction rules:     -   Select Parameter from the drop-down list and enter brand in the key value field
    -   Select Header from the drop-down list and enter account in the key value field |
    |Applicable interface|By default, this parameter is set to `/**`, which indicates that extraction rules are applicable to all business interfaces. If you need to specify an interface, enter the interface name in the field.|No|`/**`|
    |Call chain full collection|After you turn on the switch, the sample rate limit of traces is ignored and full collection is carried out. This feature is disabled by default.|No|Off|


## Query traces based on custom parameters

After you configure extraction rules for custom parameters, you can query traces based on the custom parameters.

1.  On the **Custom parameters** tab, click **Query call chain** in the right-side **Actions** column corresponding to a rule.

2.  On the **Call Chain Query** tab, configure the following parameters and click **Query**.

    **Note:** If you need to add another parameter name and value as the query condition, click the **⊕** icon to the right of the **Param Value** field in the first line.

    |Parameter|Value|
    |---------|-----|
    |Date|The time range within which traces are queried. Example: `2020-07-01 00:00 to 2020-08-01 00:00`. This parameter is specified by default.|
    |Client Name|The name of the client. This parameter is specified by default. The parameter value is not applicable in this example.|
    |Server Name|The name of the server. Select the name of the application that has extraction rules configured. This parameter is specified by default.|
    |http.parameters.brand|Example: `SIEMENS`.|
    |http.parameters.account|Example: `123456`.|

3.  Click the ID of a trace. For example, you can click the ID of a trace that is time-consuming.

4.  On the **Traces** tab, view the details of the trace and troubleshoot issues based on the information. The following table describes the displayed parameters.

    ![Method Stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7596358061/p42284.png)

    |Parameter|Description|
    |---------|-----------|
    |Application|The name of the application for which custom parameter extraction rules are configured.|
    |Log Generated At|The time when the log is generated, accurate to seconds.|
    |Status|Red indicates that an exception exists in the local trace of the service and green indicates that the trace is normal.|
    |IP Address|The IP address of the application.|
    |Call Type|The type of the call. The parameter value corresponds to the interface type of the custom parameter.|
    |Service|The name of the service. Typically, this parameter value is the interface name. You can move the pointer over the service name to check the custom parameter. For more information, see the [Verification](#section_6th_80h_mjz) section.|
    |Method Stack|After you click the magnifier icon, you can view the following information of the method stack:    -   Method: the method used to call the local method stack. After the call method is expanded, the next-layer calls of the method are displayed.
    -   Line: the line where the code of the method used to call the local method stack is located.
    -   Expanded Info:

        -   Parameter: the input parameter of the call.
        -   SQL: the SQL statement used to call the database.
        -   Exception: the error information.
    -   Timeline \(ms\): the time distribution of each method call of the local trace. |
    |Thread Profiling|The statistics on the CPU time consumption per thread and the number of each type of threads. For more information, see [Thread profiling](/intl.en-US/Application monitoring/Console functions/Application diagnosis/Thread profiling.md).|
    |Timeline \(ms\)|The time consumption of each inter-service trace and its distribution relative to that of the entire trace.|


## Verification

You can perform the following steps to verify whether the custom parameter extraction rule takes effect:

1.  On the **Traces** tab, move the pointer over a service name in the **Service** column.

2.  Check whether a custom parameter is displayed in the **Tags** section.


