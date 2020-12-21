# Add custom methods for monitoring

To monitor methods or APIs that are not detected by the Application Real-Time Monitoring Service \(ARMS\) agent, you can add custom methods for monitoring in ARMS Application Monitoring.

[Create an application monitoring job](/intl.en-US/Quick start/Create an application monitoring job.md)

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

2.  On the Applications page, click the name of the application that you want to manage.

3.  In the left-side navigation pane, click **Application Settings**. On the page that appears, click the Monitoring Method Customization tab.


## Add custom methods for monitoring

1.  On the Monitoring Method Customization tab, click **Add Method** in the upper-right corner.

2.  In the Add Custom Method dialog box, configure the following parameters and click **OK**.

    ![pg_am_settings_add_method](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1154658061/p77426.png)

    |Parameter|Description|
    |---------|-----------|
    |**Method**|The name of the method to be monitored. It must be unique.|
    |**Enable**|After you enable this feature, you can monitor this method and the method is displayed in the local method stack. For more information, see [Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md). By default, the feature is enabled.**Note:** ARMS can dynamically enable or disable this feature. Applications do not need to be restarted. |
    |**Call Entrance**|After this feature is enabled, you can query business based on traces, and the corresponding APIs are displayed in the **API call** module. For more information, see [API call monitoring](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md). By default, this feature is disabled.|

    After a custom method is added for monitoring, it is automatically displayed in the method list.


**Related topics**  


[Trace query](/intl.en-US/Application monitoring/Features provided by the console/Trace query.md)

[t152244.md\#](/intl.en-US/Application monitoring/Features provided by the console/API monitoring.md)

