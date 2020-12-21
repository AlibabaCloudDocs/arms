# Install the browser monitoring probe by using CDN

To use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor web applications, you must install the probe by using content delivery network \(CDN\) or Node Package Manager \(NPM\). This topic describes how to install the ARMS browser monitoring probe on web applications by using CDN.

## Install the browser monitoring probe

1.  In the left-side navigation pane, click **Browser Monitoring**. On the Browser Monitoring page, click **Create Application Site** in the upper-right corner.

2.  In the **Create Application Site** dialog box, select web as the monitoring type, enter the application name, and then click **OK**.

    ![Dialog Box Create New Site](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5812458061/p43513.png)

3.  Find the monitored application and click **Settings** in the **Actions** column.

4.  In the **SDK Extension Configuration** section of the settings page, select the required options. The code of the BI probe to be pasted into the page is then generated based on the selected options.

    -   **Disable Automatic API Reporting**: If you select this option, you must manually call the `__bl.api()` method to report the API success rate.
    -   **Enable Automatic SPA Parsing**: If you select this option, ARMS monitors the `hashchange` event of the page and automatically reports page views \(PVs\). This option is applied to single-page applications \(SPAs\).
    -   **Enable Data Collection of First Meaningful Paint**: If you select this option, AMRS collects data of First Meaningful Paint \(FMP\).
    -   **Enable Page Resources Reporting**: If you select this option, static resources loaded on the page are reported when the onload event is triggered.
    -   **Associate with Application Monitoring**: If you select this option, API requests are in end-to-end association with application monitoring.
    -   **Enable User Behavior Trace**: If you select this option, you can view user behavior trace in JS Error Diagnosis.

        **Note:**

    -   **Enable Console Tracing**: If you select this option, user behavior is traced in the console. The behavior can be `error`, `warn`, `log`, or `info`.

        **Note:** This feature affects the path of the Console panel.

5.  Install the probe by using one of the following methods:

    -   Asynchronous loading: copy the provided code, paste it to the first line of the `<body>` element of the HTML page, and then restart the application.

        ![tab_bm_async_load](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5812458061/p120732.png)

    -   Synchronous loading: copy the provided code, paste it to the first line of the `<body>` element of the HTML page, and then restart the application.

        ![tab_bm_sync_load](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5812458061/p120734.png)

    -   npm package:
        1.  Run the following command to install the npm package:

            ```
            npm install alife-logger --save
            ```

        2.  Copy and run the following command from the console to initialize the npm package:

            ```
            const BrowserLogger = require('alife-logger');
            const __bl = BrowserLogger.singleton({pid:"b590lhguqs@8cc3f63543d****",appType:"web",imgUrl:"https://arms-retcode.aliyuncs.com/r.png?",sendResource:true,behavior:true,enableLinkTrace:true,enableConsole:true});
            ```


## Differences between asynchronous loading and synchronous loading

-   Asynchronous loading: It is also known as non-blocking loading. In asynchronous loading, the browser does continue to process subsequent pages after the JS loading is complete. We recommend that you use this method if you require high page performance.

    **Note:** If you use asynchronous loading, ARMS cannot capture JS errors or resource loading errors before the monitoring SDK completes the initialization.

-   Synchronous loading: It is also known as blocking loading. In synchronous loading, the browser does not continue to process subsequent pages until the JS loading is complete. We recommend that you use synchronous loading if you need to capture JS errors and resource loading errors during the whole process.

## Custom UID

When the ARMS browser monitoring probe is installed by using synchronous or asynchronous loading, the web SDK automatically generates a user ID \(UID\) to collect information such as the number of unique visitors \(UVs\). The UID can be used to identify a user but does not have service attributes. If you want to customize a UID, add the following content to `config` in the code:

```
uid: 'xxx', // The UID is used to identify a user. You can specify the UID based on your business requirements.
```

Sample code:

```
<script>
!( function(c,b,d,a){c[a]||(c[a]={});c[a].config={pid:"xxx",appType:undefined,imgUrl:"https://arms-retcode.aliyuncs.com/r.png?", uid: "xxxx"};
with(b)with(body)with(insertBefore(createElement("script"),firstChild))setAttribute("crossorigin","",src=d)
})(window,document,"https://retcode.alicdn.com/retcode/bl.js","__bl");
</script>
```

**Note:** If you modify options in the SDK Extension Configuration section, the code changes. Copy and paste the code again.

## Common SDK parameters

The browser monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet your business requirements. The following table lists the common parameters that you can specify in the scenarios described in this topic. |
| |
| |
| |
| |
| |

The browser monitoring feature of ARMS also provides more SDK configuration items to further meet your requirements. For more information, see [SDK reference](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

**Related topics**  


[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

[SDK reference](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md)

[Implement browser monitoring by using npm](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For Web applications/Install the ARMS agent through npm.md)

[Implement browser monitoring in the Weex environment](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For Weex/Perform browser monitoring in the Weex environment.md)

