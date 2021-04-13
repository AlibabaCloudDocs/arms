# Install the browser monitoring probe by using CDN

To use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor web applications, you must install the probe by using Alibaba Cloud Content Delivery Network \(CDN\) or node package manager \(npm\). This topic shows you how to install the ARMS browser monitoring probe on web applications by using CDN.

## Install the browser monitoring probe

1.  Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Browser Monitoring**. On the Browser Monitoring page, click **Create Application Site** in the upper-right corner.

3.  In the **Create Application Site** dialog box, select web as the monitoring type, enter the application name, and then click **OK**.

    ![Dialog Box Create New Site](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5812458061/p43513.png)

4.  On the settings page of the application, select the required options in the **SDK Extension Configuration** section. The code of the BI probe to be pasted to the page is then generated based on the selected options.

    -   **Disable Automatic API Reporting**: If you select this option, you must manually call the `__bl.api()` method to report the API success rate.
    -   **Enable Automatic SPA Parsing**: If you select this option, ARMS monitors the `hashchange` event of the page and automatically reports page views \(PVs\). This option is applied to single-page applications \(SPAs\).
    -   **Enable Data Collection of First Meaningful Paint**: If you select this option, ARMS collects data of First Meaningful Paint \(FMP\).
    -   **Enable Page Resources Reporting**: If you select this option, static resources loaded on the page are reported when the onload event is triggered.
    -   **Associate with Application Monitoring**: If you select this option, API requests are in end-to-end association with application monitoring.
    -   **Enable User Behavior Trace**: If you select this option, you can view user behavior trace in JS Error Diagnosis.
    -   **Enable Console Tracing**: If you select this option, user behavior is traced in the console. The behavior can be `error`, `warn`, `log`, or `info`.

        **Note:** This feature affects the path of the Console panel.

5.  Install the probe by using one of the following methods:

    -   Asynchronous loading: Copy the provided code, paste it to the first line of the `<body>` element of the HTML page, and then restart the application.

        ![tab_bm_async_load](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5812458061/p120732.png)

    -   Synchronous loading: Copy the provided code, paste it to the first line of the `<body>` element of the HTML page, and then restart the application.

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

-   Asynchronous loading: It is also known as non-blocking loading. In asynchronous loading, the browser continues to process subsequent pages no matter whether JavaScript loading is complete. We recommend that you use this method if you require high page performance.

    **Note:** If you use asynchronous loading, ARMS cannot capture JavaScript errors or resource loading errors before the monitoring SDK completes the initialization.

-   Synchronous loading: It is also known as blocking loading. In synchronous loading, the browser does not continue to process subsequent pages until the JavaScript loading is complete. We recommend that you use synchronous loading if you need to capture JavaScript errors and resource loading errors during the whole process.

## Custom UID

When the ARMS browser monitoring probe is installed by using synchronous or asynchronous loading, the web SDK automatically generates a user ID \(UID\) to collect information such as the number of unique visitors \(UVs\). The UID can be used to identify a user but does not have business attributes. If you want to customize a UID, add the following content to `config` in the code:

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

The browser monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet additional requirements. The following table describes the common parameters that you can specify in the scenarios described in this topic.

|Parameter|Type|Description|Required|Default Value|
|---------|----|-----------|--------|-------------|
|pid|String|The unique ID of the project, which is automatically generated by ARMS when it creates the site.|Yes|N/A|
|uid|String|The user ID, which identifies the user and can be manually configured to be retrieved based on the user ID. If you do not configure the settings, they are automatically generated by the SDK and updated semi-annually.|No|Automatically generated by SDK|
|tag|String|The input tag. Each log carries a tag.|No|None|
|release|String|The version of the application. We recommend that you configure to view the reports of different versions.|No|`undefined`|
|environment|String|The environment field. Valid values: prod, gray, pre, daily, and local, where: -   prod indicates an online environment.
-   gray indicates a phased-release environment.
-   pre indicates a staging environment.
-   daily indicates a daily environment.
-   local indicates a local environment.

|No|`prod`|
|sample|Integer|The log sampling configuration. The value is an integer ranging from 1 to 100. For performance logs and successful API logs, follow the steps in `1/sample`The proportional sampling of. For more information about metrics descriptions of performance logs and successful API logs, see [Statistical metrics](/intl.en-US/Browser Monitoring/Statistical metrics.md).|No|`1`|
|behavior|Boolean|Whether to record the error user behavior to facilitate troubleshooting.|No|`true`|
|enableSPA|Boolean|Listen to the hashchange event on the page and report the PV again. This method is applicable to single-page application scenarios.|No|`false`|
|enableLinkTrace|Boolean|For more information about tracing frontend and backend links, see [t152278.md\#](/intl.en-US/Browser Monitoring/Tutorials/Use the front-to-back tracing feature to diagnose causes of API errors.md).|No|`false`|

The browser monitoring feature of ARMS also provides more SDK parameters to further meet your requirements. For more information, see [SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md).

**Related topics**  


[Browser monitoring overview](/intl.en-US/Browser Monitoring/Quick start/Browser monitoring overview.md)

[SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md)

[Implement browser monitoring by using npm](/intl.en-US/Browser Monitoring/Quick start/For Web applications/Implement browser monitoring by using npm.md)

[Implement browser monitoring in the Weex environment](/intl.en-US/Browser Monitoring/Quick start/For Weex/Implement browser monitoring in the Weex environment.md)

