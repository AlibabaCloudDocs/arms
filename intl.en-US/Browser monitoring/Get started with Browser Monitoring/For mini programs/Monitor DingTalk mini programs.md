# Monitor DingTalk mini programs

This topic describes how to use the browser monitoring function of Application Real-Time Monitoring Service \(ARMS\) to monitor [DingTalk mini programs](https://open-doc.dingtalk.com/microapp/dev/ed25rr). It also demonstrates the general configurations, methods, and advanced scenarios.

## Procedure

To monitor the mini programs, you need to perform at least the three steps: introducing and initializing the Node Package Manager \(NPM\) package, reporting logs, and setting security domains.

1.  Introduce and initialize the NPM package.

    1.  Introduce the NPM package named alife-logger in the DingTalk mini program project to facilitate log reporting.

        ```
        npm install alife-logger                      
        ```

    2.  Add the following information to the monitor.js file in the /utils directory to initialize the NPM package.

        **Note:** You can specify the name and storage path of the JS file.

        ```
        import EAppLogger from 'alife-logger/eapp';
        const Monitor = EAppLogger.init({
            pid: 'xxx',
            region: "cn", // The region where the application is deployed. Set it to cn if the application is deployed in China, to sg if the application is deployed near Singapore outside China, and to us if the application is deployed near the United States outside China.
        });
        
        export default Monitor;            
        ```

        **Note:** For more information about parameter configurations, see [Common parameters](#Configuration).

2.  Call the following methods to automatically collect the page view \(PV\), error, API request, performance, and health data.

    1.  In app.js, call Monitor.hookApp\(options\) to automatically capture error logs. The options parameter is the app-specific object.

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

    2.  In page.js, call Monitor.hookPage\(options\) to automatically report the API request, PV, and health data.

        ```
        import Monitor from '/util/monitor';
        // After hookPage is called, the lifecycle API automatically starts instrumentation.
        Page(Monitor.hookPage({
           data: {},
            onLoad(query) {
            },
            onReady() {
            // Page loaded.
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

    -   If the region is set to `cn`, add arms-retcode.aliyuncs.com to the HTTP security domain of the request.
    -   If the region is set to `sg`, add arms-retcode-sg.aliyuncs.com to the HTTP security domain of the request.

## Common parameters

The following table lists the common parameters that are used for initializing the NPM package.

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|pid|String|The ID of the site.|Yes|null|
|uid|String|The ID of the user, which is used to collect the unique visitor \(UV\) data.|No|Storage setting|
|tag|String|The input tag. Each log carries a tag.|No|None|
|disabled|Boolean|Specifies whether the log reporting function is disabled.|No|false|
|sample|Integer|The log sampling rate. Valid values: 1, 10, and 100. Performance logs and successful API request logs are reported in a 1/number of samples ratio.|No|1|
|enableLinkTrace|Boolean|Specifies whether front-to-back tracing is supported.|No|false|
|disableHook|Boolean|Specifies whether to disable monitoring dd.httpRequest. By default, the request is monitored, and the request success rate is reported.|No|false|
|sendRequest|Function|The method for sending logs. If this parameter is not configured, the default value dd.httpRequest is used.|No|dd.httpRequest|
|getCurrentPage|Function|The method for obtaining the current page.|No|getCurrentPage|

## Basic methods for automatic instrumentation

|Method|Parameter|Remarks|Scenario|
|------|---------|-------|--------|
|hookApp|\{\}|Enter the source app parameters.|The app lifecycle API automatically starts instrumentation.|
|hookPage|\{\}|Enter the source page parameters.|The page lifecycle API automatically starts instrumentation.|

**Note:** If the lifecycle API calls the hookApp or hookPage method for instrumentation in mini program monitoring projects, the projects must conform to the app and page regulations of standard mini programs. In other words, the projects must support **onError** under App, and **onShow**, **onHide**, and **onUnload** under Page. For usage examples, see [Procedure](#section_vgv_cp2_jhb).

## Methods for other settings

|Method|Parameter|Remarks|
|------|---------|-------|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for the scenarios such as phased release.|
|setConfig|\{\[key: string\]: string;\}|Set the config field.|
|pageShow|\{\}|Report the PV data.|
|pageHide|\{\}|Report the health data.|
|error|String/Object|Report error logs.|
|api|See also [t152281.md\#section\_k3o\_jn0\_k38](/intl.en-US/Browser monitoring/API reference.md)|Report the API request logs.|
|sum/avg|String|Report the custom sum and average logs.|

## Advanced scenarios

When the basic usage cannot meet your needs, see the following advanced scenarios.

-   Manually report the API request results \(automatic reporting is disabled\).

    1.  Set disableHook to `true`. The logs of the dd.httpRequest request are not reported automatically.
    2.  Manually call api\(\) to report the API request results.
-   Disable automatic reporting and enable manual instrumentation.

    1.  No longer use the hookApp and hookPage methods in the app.js and page.js files.

    2.  To send the PV data of the current page, call pageShow\(\) under onShow of Page.

        **Note:** Do not call pageShow\(\) together with hookPage\(\). Otherwise, the PV logs are reported repeatedly.

        ```
        import Monitor from '/util/monitor';
        Page({
            onShow: function() {
                Monitor.pageShow();
            }
        })                         
        ```

    3.  To send the health data \(health and browsing time\) of the current page, call pageHide\(\) under onHide and onUnload of Page.

        **Note:** Do not call pageHide\(\) together with hookPage\(\). Otherwise, the logs are reported repeatedly.

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


## More information

-   [Overview](/intl.en-US/Browser monitoring/Overview.md)
-   [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor Alipay mini programs.md)
-   [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor WeChat mini programs.md)
-   [Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For mini programs/Monitor other mini programs.md)

