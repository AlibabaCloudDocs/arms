# Monitor DingTalk mini programs

This topic describes how to use the frontend monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor DingTalk mini programs. This topic also describes the general configurations, methods, and advanced scenarios of the feature.

## Background information

For more information about DingTalk mini programs, see the [documentation of DingTalk mini programs](https://open-doc.dingtalk.com/microapp/dev/ed25rr).

## Procedure

To monitor a DingTalk mini program, install and initialize the npm package, report the monitoring data, and then configure security domains.

1.  Install and initialize the npm package.
    1.  Install the npm package named alife-logger in the DingTalk mini program. This module can then be used to report logs.

        ```
        npm install alife-logger                      
        ```

    2.  Add the following code to the monitor.js file in the /utils directory to initialize the npm package.

        **Note:** You can specify the name and storage path of the JS file.

        ```
        import EAppLogger from 'alife-logger/eapp';
        const Monitor = EAppLogger.init({
            pid: 'xxx',
            region: "cn", // The region where the mini program is deployed. Set the region parameter to cn if the mini program is deployed in China. Set the region parameter to sg if the mini program is deployed in or near Singapore. Set the region parameter to us if the mini program is deployed in or near the United States. 
        });
        
        export default Monitor;            
        ```

        **Note:** For more information about parameter settings, see [Common SDK parameters](#section_vo9_hoe_9w4).

2.  Use the following methods to automatically collect and report the logs about page views \(PVs\), errors, API requests, performance, and health.
    1.  In the app.js file, call the `Monitor.hookApp(options)` method to automatically capture error logs. The options parameter is an app-specific object.

        ```
        import Monitor from '/util/monitor';
        
        App(Monitor.hookApp({
          onError(err) {
              console.log('Trigger onError:', err);
          },
          onLaunch() {
            console.log('Trigger onLaunch');
          },
        
          onShow(options) {
          },
          onHide() {
          }
        }));                         
        ```

    2.  In the page.js file, call the `Monitor.hookPage(options)` method to automatically report the logs about API requests, PVs, and health.

        ```
        import Monitor from '/util/monitor';
        // After you call the hookPage method, the lifecycle-based API automatically starts instrumentation. 
        Page(Monitor.hookPage({
           data: {},
            onLoad(query) {
            },
            onReady() {
            // The page is loaded. 
            },
            onShow() {
        
            },
            onLoad(query) {
        
            },
            onHide() {
        
            },
            onUnload() {
        
            }     
        }));                        
        ```

3.  Set security domains.
    -   If the region parameter is set to `cn`, add arms-retcode.aliyuncs.com to the HTTP security domain.
    -   If the region parameter is set to `sg`, add arms-retcode-sg.aliyuncs.com to the HTTP security domain.

## Basic methods for automatic instrumentation

|Method|Parameter|Description|Scenario|
|------|---------|-----------|--------|
|hookApp|\{\}|Enter the source app parameters.|Perform automatic instrumentation during the lifecycle of the app.|
|hookPage|\{\}|Enter the source page parameters.|Perform automatic instrumentation during the lifecycle of the page.|

**Note:** If you want to call the hookApp or hookPage method for instrumentation in mini program monitoring projects, the projects must conform to the app and page regulations of standard mini programs. The projects must support the onError method for apps, and the onShow, onHide, and onUnload methods for pages. For examples of the methods, see [Procedure](#section_vgv_cp2_jhb).

## Methods for other settings

|Method|Parameter|Description|
|------|---------|-----------|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for scenarios such as canary release.|
|setConfig|\{\[key: string\]: string;\}|Set the config field. For more information about the operation, see [SDK configuration items parameters](https://www.alibabacloud.com/help/zh/doc-detail/58655.htm#title-ps9-1pa-qg5).|
|pageShow|\{\}|Report the PV logs.|
|pageHide|\{\}|Report the health logs.|
|error|String/Object|Report error logs.|
|api|For more information, see [API reference](/intl.en-US/Browser Monitoring/API reference.md).|Report the API request logs.|
|sum/avg|String|Report the custom sum and average logs.|

## Advanced scenarios

If the basic methods cannot meet your needs, see the following advanced scenarios:

-   Manually report the API request results. Automatic reporting is disabled.

    1.  Set the disableHook parameter to `true`. The logs of the dd.httpRequest method are not automatically reported.
    2.  Manually call the `api` method to report the API request results.
-   Disable automatic reporting and enable manual instrumentation.

    1.  The `hookApp` and `hookPage` methods are no longer used in the app.js and page.js files.

    2.  To report the PV logs of the page, call the `pageShow` method in the `onShow` method.

        **Note:** Do not call the pageShow method together with the `hookPage` method. Otherwise, the PV logs are repeatedly reported.

        ```
        import Monitor from '/util/monitor';
        Page({
            onShow: function() {
                Monitor.pageShow();
            }
        })                         
        ```

    3.  To report the health logs that indicate the health level and browsing time on the page, call the `pageHide` method in the `onHide` and `onUnload` methods.

        **Note:** Do not call the pageHide method together with the `hookPage` method. Otherwise, the logs are repeatedly reported.

        ```
        import Monitor from '/util/monitor';
          Page({
        
              onHide: function() {
                  Monitor.pageHide();
              },
              onUnload: function() {
                  Monitor.pageHide();
              }
              ... 
          })                    
        ```


## Common SDK parameters

The frontend monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet additional requirements. The following table describes the common parameters suitable for the scenarios described in this topic.

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
|behavior|Boolean|Whether to record the error user behavior to facilitate troubleshooting.|No|`false`|
|enableLinkTrace|Boolean|For more information about tracing frontend and backend links, see [t152278.md\#](/intl.en-US/Browser Monitoring/Tutorials/Use the front-to-back tracing feature to diagnose API errors.md).|No|`false`|

The ARMS frontend monitoring feature also provides other SDK parameters to meet your business requirements. For more information, see [SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md).

[What is ARMS Browser Monitoring?](/intl.en-US/Browser Monitoring/What is ARMS Browser Monitoring?.md)

[Monitor Alipay mini programs](/intl.en-US/Browser Monitoring/Quick start/For mini programs/Monitor Alipay mini programs.md)

[Monitor WeChat mini programs](/intl.en-US/Browser Monitoring/Quick start/For mini programs/Monitor WeChat mini programs.md)

[Monitor other mini programs](/intl.en-US/Browser Monitoring/Quick start/For mini programs/Monitor other mini programs.md)

