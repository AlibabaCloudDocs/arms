# Add custom methods for monitoring

To monitor any methods or APIs that are not automatically detected by the Application Real-Time Monitoring Service \(ARMS\) agent, you can add custom methods for monitoring in ARMS Application Monitoring.

[Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)

## Portal

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**.

3.  On the Applications page, click the name of the target application.

4.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Monitoring Method Customization tab.


## Add custom methods for monitoring

1.  On the Monitoring Method Customization tab, click **Add Method** in the upper-right corner.

2.  In the Add Custom Method dialog box, create a custom method and click **OK**.

    |Parameter|Description|
    |---------|-----------|
    |**Method**|The name of the method to be monitored. It must be unique.|
    |**Enable**|After you enable this feature, you can monitor this method and the method is displayed in the local method stack. For more information, see [Related operations](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md). By default, the feature is enabled. **Note:** ARMS can dynamically enable or disable this feature, without restarting the application. |
    |**Call Entrance**|After this feature is enabled, you can query businesses based on traces, and the corresponding APIs are displayed in the **API call** module. For more information, see [t152244.md\#](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md). By default, this feature is disabled.|

    ![pg_am_settings_add_method](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1154658061/p77426.png)

    After a custom method is added for monitoring, it is automatically displayed in the method list.


[Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md)

[t152244.md\#](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md)

