# Monitor WeChat mini programs

This topic describes how to use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor WeChat mini programs and introduces the common SDK configurations, API operations, and advanced scenarios of the browser monitoring feature.

## Background information

For more information about WeChat mini programs, visit [WeChat mini programs](https://developers.weixin.qq.com/miniprogram/dev/framework/).

## Basic usage

To monitor a WeChat mini program, you must perform the following basic steps:

1.  Obtain and initialize the monitoring SDK for WeChat mini programs.

    1.  Copy the content of the [JS file](https://retcode.alicdn.com/retcode/wl.js) and paste the content to the wxLogger.js file in the /utils folder of the WeChat mini program that you want to monitor.

    2.  Add the following content to the monitor.js file in the /utils folder of the WeChat mini program to initialize the monitoring SDK.

        **Note:** You can specify the name of the JS file and the path used to store the file.

        -   If the project is integrated by using the node module \(require\) method, add the following content to the monitor.js file:

            ```
            const WXLogger = require('./wxLogger.js');
                const Monitor = WXLogger.init({
                    pid: 'xxx',
                    region: 'cn'
                });
                export default Monitor;
            ```

        -   If the project is integrated by using the ES module \(import\) method, add the following content to the monitor.js file:

            ```
            import WXLogger from './wxLogger.js';
                const Monitor = WXLogger.init({
                    pid: 'xxx',
                    region: 'cn'
                });
                export default Monitor;
            ```

        **Note:** For more information about parameter configurations, see [Common SDK parameters](#section_vo9_hoe_9w4).

2.  Use the following methods to automatically collect the PV, error, API, performance, and health data of the WeChat mini program:

    1.  In app.js, call **Monitor.hookApp\(options\)** to automatically capture error logs. The **options** parameter is the object settings in the app.

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

    2.  In page.js, call **Monitor.hookPage\(options\)** to automatically report the API, PV, and health data of the WeChat mini program.

        ```
        import Monitor from '/util/monitor';
        // After you call hookPage, the lifecycle-based API automatically starts instrumentation.
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

3.  Set security domain names.

    -   If **region** is set to `cn`, add `https://arms-retcode.aliyuncs.com` to the valid domain names of the request.

    -   If **region** is set to `sg`, add `https://arms-retcode-sg.aliyuncs.com` to the valid domain names of the request.


## Basic methods for automatic instrumentation

|Method|Parameter|Description|Scenario|
|------|---------|-----------|--------|
|hookApp|\{\}|Uses the parameters of App.|Perform automatic instrumentation during the lifecyle of App.|
|hookPage|\{\}|Uses the parameters of Page.|Perform automatic instrumentation during the lifecyle of Page.|

**Note:** If you want to use the hookApp and hookPage methods in the monitoring project of your WeChat mini program for instrumentation during the lifecycle of App and Page, the hookApp method must include **onError** and the hookPage method must include **onShow**, **onHide**, and **onUnload**. For more information about how to use these methods, see [Basic usage](#section_dxs_ls2_jhb)

## Methods for other settings

|Method|Parameter|Description|
|------|---------|-----------|
|setCommonInfo|\{\[key: string\]: string;\}|Sets basic log fields in scenarios such as canary release.|
|setConfig|\{\[key: string\]: string;\}| |
|pageShow|\{\}|Reports the PV data.|
|pageHide|\{\}|Reports the health data.|
|error|String/Object|Reports error logs.|
|api|For more information, see [API reference](/intl.en-US/Browser monitoring/Methods user guide.md).|Reports API request logs.|
|sum/avg|String|Reports the custom sum and average logs.|

## Advanced scenarios

When the basic usage of application monitoring cannot meet your requirements, try the usage in the following advanced scenarios:

-   Manually report the API request results.

    1.  Set **disableHook** to `true`. The logs of the **wx.request** request are not automatically reported.

    2.  Manually call **api\(\)** to report the API request results.

-   Disable automatic reporting and enable manual instrumentation.

    1.  Do not use the hookApp and hookPage methods in the app.js and page.js files.

    2.  To send the PV data of the current page, call **pageShow\(\)** in the **onShow** method of Page.

        **Note:** Do not call pageShow\(\) together with **hookPage\(\)**. Otherwise, the PV logs are reported repeatedly.

        ```
        import Monitor from '/util/monitor';
        Page({
            onShow: function() {
                Monitor.pageShow();
            }
        })
        ```

    3.  To send the health data including the health and browsing time of the current page, call **pageHide\(\)** under the **onHide** and **onUnload** methods of Page.

        **Note:** Do not call pageHide\(\) together with **hookPage\(\)**. Otherwise, the logs are reported repeatedly.

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

The browser monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet more requirements. The following table describes the parameters that you can configure in the scenarios described in this topic. |
| |
| |
| |
| |
|

For more information about the SDK parameters that you can configure, see [SDK reference](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

**Related topics**  


[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

[Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md)

[Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md)

[Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor other mini programs.md)

