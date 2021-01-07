# Monitor DingTalk mini programs

This topic describes how to use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor DingTalk mini programs. This topic also describes the general configurations, API methods, and advanced scenarios.

## Background information

For background information about the DingTalk mini program, see [DingTalk mini program](https://open-doc.dingtalk.com/microapp/dev/ed25rr)Migrate an instance across regions based on Global Replica.

## Procedure

To monitor a DingTalk mini program, install and initialize the Node Package Manager \(NPM\) package, report monitoring data, and then configure security domains.

1.  Install and initialize the NPM package.
    1.  Install the NPM package named alife-logger in the DingTalk mini program. This module can then be used to report logs.

        ```
        npm install alife-logger                      
        ```

    2.  Add the following to /utilsDirectory in the monitor.js file to complete the initialization.

        **Note:** You can specify the name and storage path of the JavaScript \(JS\) file.

        ```
        import EAppLogger from 'alife-logger/eapp';
        const Monitor = EAppLogger.init({
            pid: 'xxx',
            region: "cn",
        });
        
        export default Monitor;            
        ```

        **Note:** For detailed configuration of parameters, see [Common parameters of SDK](#section_vo9_hoe_9w4).

2.  You can use the following methods to automatically collect and report page views \(PVs\), error, API requests, performance, and health data.
    1.  In app.js, use the Monitor.hookApp\(options\)Method silently captures the Error class log. Of which optionsThat is, the corresponding Object configuration for the App layer.

        ```
        import Monitor from '/util/monitor';
        
        App(Monitor.hookApp({
          onError(err) {
              console.log('onError:', err);
          },
          onLaunch() {
            console.log('onLaunch');
          },
        
          onShow(options) {
          },
          onHide() {
          }
        }));                         
        ```

    2.  In the JS file of the Page by Monitor.hookPage\(options\)Method to silently report the API request, PV, and Health data.

        ```
        import Monitor from '/util/monitor';
        
        Page(Monitor.hookPage({
           data: {},
            onLoad(query) {
            },
            onReady() {
        
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
    -   If regionSet as `cn`, add the arms-retcode.aliyuncs.com to the HTTP security Domains.
    -   If regionSet as `sg`, add the arms-retcode-sg.aliyuncs.com to the HTTP security Domains.

## Basic API methods for automatic tracking

|Method|Parameter|Description|Scenario|
|------|---------|-----------|--------|
|hookApp|\{\}|Enter the parameters of the application.|API lifecycle management automatically tracks the application.|
|hookPage|\{\}|Enter the parameters of the page.|API lifecycle management automatically tracks the page.|

**Note:** For mini program monitoring items that need to use hookApp and hookPage to embed lifecycle hitting points, they must comply with the standard Mini program specifications on apps and pages. That is, the App layer has **onError**, the Page layer has **onShow**, **onHide**, **onUnload**. For usage examples, see [Procedure](#section_vgv_cp2_jhb).

## Other API methods

|Method|Parameter|Description|
|------|---------|-----------|
|setCommonInfo|\{\[key: string\]: string;\}|Set basic log fields for scenarios such as phased release.|
|setConfig|\{\[key: string\]: string;\}|Set the config field. For more information, see . Configure configuration items parameters|
|pageShow|\{\}|Report the PV data.|
|pageHide|\{\}|Report the health data.|
|error|String/Object|Report error logs.|
|api|For more information, [API reference](/intl.en-US/Browser monitoring/API reference.md)|Report the API request logs.|
|sum/avg|String|Report custom sum and average logs.|

## Advanced scenarios

If the basic methods cannot meet your needs, see the following advanced scenarios:

-   Manually report the API operations. Automatic reporting is disabled.

    1.  Soon disableHookSet as `true`, not reported silently dd.httpRequestThe requested log.
    2.  Manually called api\(\)Method to report API-related information.
-   Disable automatic reporting and enable manual tracking.

    1.  No longer used in App and Page JS files. hookApp, hookPageMethod.

    2.  To send the PV data of the current Page, on the Page onShowCall under method pageShow\(\)Method.

        **Note:** Do not interact with hookPage\(\)Method uses this method at the same time. Otherwise, PV logs may be reported repeatedly.

        ```
        import Monitor from '/util/monitor';
        Page({
            onShow: function() {
                Monitor.pageShow();
            }
        })
        ```

    3.  To send Health-class data for the current Page, statistics on the Health of the current Page and Page stay time, on the Page onHideand onUnloadCall under method pageHide\(\)Method.

        **Note:** Do not interact with hookPage\(\)METHOD. This method is used at the same time. Otherwise, repeated log reporting may occur.

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

ARMS browser monitoring provides a series of SDK parameters. You can configure the parameters to meet additional requirements. The following table describes the common parameters suitable for the scenarios described in this topic.

|Parameter|Type|Description|Required|Default Value|
|---------|----|-----------|--------|-------------|
|pid|String|The unique ID of the project, which is automatically generated when ARMS creates the site.|Yes|No default value|
|uid|String|The user ID, which is used to identify the user. You can manually configure the ID to search for the user based on the user ID. If this parameter is not configured, the updates are automatically generated by the SDK and updated every six months.|No|Generated by the SDK|
|tag|String|The input tag. Each log carries a tag.|No|No default value|
|release|String|The version of the application. We recommend that you configure to view the reports of different versions.|No|`undefined`|
|environment|String|The production environment. Valid values: prod, gray, pre, daily, and local. -   prod indicates the online environment.
-   gray indicates the grayscale environment.
-   pre: the staging environment.
-   daily indicates the daily environment.
-   local indicates the local environment.

|No|`prod`|
|sample|Integer|The sampling configuration of the log. The value ranges from 1 to 100. Sample Performance logs and successful API logs in accordance with the `1/sample` ratio. For more information about the metrics of performance logs and successful API logs, see [Statistical metrics](/intl.en-US/Browser monitoring/Statistical metrics.md).|No|`1`|
|behavior|Boolean|Whether to record the user behavior to facilitate troubleshooting.|No|`false`|
|enableLinkTrace|Boolean|For more information about front-to-back tracing, see [t152278.md\#](/intl.en-US/Browser monitoring/Tutorials/Use the front-to-back tracing feature to diagnose causes of API errors.md).|No|`false`|

ARMS browser monitoring also provides other SDK parameters. For more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

[Overview](/intl.en-US/Browser monitoring/Overview.md)

[Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor Alipay mini programs.md)

[Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor WeChat mini programs.md)

[Monitor other mini programs](/intl.en-US/Browser monitoring/Get started with browser monitoring/For mini programs/Monitor other mini programs.md)

