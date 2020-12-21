# Monitor Alipay mini programs

This topic describes how to use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor Alipay mini programs and introduces the common SDK configurations, API operations, and advanced scenarios of the browser monitoring feature.

## Background information

For more information, see [https://docs.alipay.com/mini/developer/getting-started](https://docs.alipay.com/mini/developer/getting-started)

## Basic usage

To monitor mini programs, you must perform the following operations to introduce and initialize the npm package, report logs, and set security domain names.

1.  Introduce and initialize the npm package.

    1.  In your mini program project, introduce the npm package named `alife-logger` to facilitate log reporting.

        ```
        npm install alife-logger
        ```

    2.  Add the following information to the monitor.js file in the /utils directory to initialize the package.

        **Note:** You can specify the name and storage path of the JavaScript \(JS\) file.

        ```
        import AlipayLogger from 'alife-logger/alipay';
        const Monitor = AlipayLogger.init({
            pid: 'xxx',
            region: 'cn', // The region where the application is deployed. Set region to cn if the application is deployed in China and set region to sg if the application is deployed outside China.
        });
        
        export default Monitor;              
        ```

        **Note:** For more information about parameter settings, see [Common parameters of SDK](#section_vo9_hoe_9w4).

2.  Use the following methods to automatically collect the PV, error, API, performance, and health data of the Alipay mini program:

    1.  In the app.js file, call the **Monitor.hookApp\(options\)** method to automatically capture error logs. The **options** parameter is the app-specific object.

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

    2.  In page.js, call **Monitor.hookPage\(options\)** to automatically report the API, PV, and health data of the Alipay mini program.

        ```
        import Monitor from '/util/monitor';
        // After the hookPage method is called, API lifecycle management automatically tracks.
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

    -   If **region** is set to `cn`, add arms-retcode.aliyuncs.com to the HTTP security domain.

    -   If **region** is set to `sg`, add arms-retcode-sg.aliyuncs.com to the HTTP security domain.


## Basic API methods for automatic tracking

|Method|Parameter|Description|Scenario|
|------|---------|-----------|--------|
|hookApp|\{\}|Enter the parameters of the application.|API lifecycle management automatically tracks the application.|
|hookPage|\{\}|Enter the parameters of the page.|API lifecycle management automatically tracks the page.|

**Note:** If you want to call the hookApp or hookPage method to track and monitor mini programs, the code must conform to the app and page specifications of standard mini programs. The **onError** method must be included in the code of the application. The **onShow**, **onHide**, and **onUnload** methods must be included in the code of the page. For more information, see [Basic usage](#section_upb_2q2_jhb).

## Other API methods

|Method|Parameter|Description|
|------|---------|-----------|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for the scenarios such as phased release.|
|setConfig|\{\[key: string\]: string;\}| |
|pageShow|\{\}|Report PV data.|
|pageHide|\{\}|Report health data.|
|error|String/Object|Report error logs.|
|api|For more information, see [API reference](/intl.en-US/Browser monitoring/Methods user guide.md).|Report API logs.|
|sum/avg|String|Report custom sum and average logs.|

## Advanced scenarios

If the basic usage cannot meet your requirements, refer to the following advanced scenarios:

-   Manually report the API request results.

    1.  Set **disableHook** to `true`. The logs of **my.httpRequest** are not automatically reported.

    2.  Manually call the **api\(\)** method to report the API operations.

-   Disable automatic reporting and enable manual tracking.

    1.  Do not use the hookApp and hookPage methods in the app.js and page.js files.

    2.  To send the PV data of the page, call the **pageShow\(\)** method in the **onShow** method.

        **Note:** We recommend that you do not call the pageShow\(\) method together with the **hookPage\(\)** method. Otherwise, the PV logs are repeatedly reported.

        ```
        import Monitor from '/util/monitor';
        Page({
            onShow: function() {
                Monitor.pageShow();
            }
        })
        ```

    3.  To send the health data \(health and browsing time\) of the page, call the **pageHide\(\)** method in the **onHide** and **onUnload** methods.

        **Note:** We recommend that you do not call the pageHide\(\) method together with the **hookPage\(\)** method. Otherwise, the logs are repeatedly reported.

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


## Common parameters of SDK

ARMS browser monitoring provides a series of SDK parameters. You can configure the parameters to meet additional requirements. The following table describes the common parameters suitable for the scenarios described in this topic. |
| |
| |
| |
| |
|

ARMS browser monitoring also provides other SDK parameters. For more information, see [SDK reference](/intl.en-US/Browser monitoring/Configuration items of the browser monitoring SDK.md).

**Related topics**  


[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

[Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor DingTalk mini programs.md)

[Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md)

[Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor other mini programs.md)

