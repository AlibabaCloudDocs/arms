# Implement browser monitoring by using npm

To use the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) to monitor web applications, you must install the ARMS agent by using Content Delivery Network \(CDN\) or Node Package Manager \(npm\). This topic describes how to use npm to install the ARMS browser monitoring agent for web applications.

## Install the npm package

Install the npm package named `alife-logger`.

```
npm install alife-logger --save
```

## Initialize the SDK

Use `BrowserLogger.singleton` to initialize the SDK.

```
const BrowserLogger = require('alife-logger');
                // Use BrowserLogger.singleton(conf) config to load the configurations specified by config.
                const __bl = BrowserLogger.singleton({
                pid: 'your-project-id',
                // Specify the path to which the logs are uploaded.
                // If you want to deploy the SDK in the Singapore region, set the path to https://arms-retcode-sg.aliyuncs.com/r.png?.
                // If you want to deploy the SDK in the US (Silicon Valley) region, set the path to http://arms-us-west-1.console.aliyun.com/r.png?.
                imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', 
                // Set other configurations specified by config.
                });
```

When the ARMS browser monitoring agent is installed by using npm, the SDK automatically generates a user ID \(UID\) to collect information such as the number of unique visitors \(UVs\). The generated UIDs can be used to identify users but does not have service attributes. If you want to customize a UID, add the following content to the code:

```
uid: 'xxx', // The UID is used to identify a user. Set its value based on your businesses.
```

Example:

```
const BrowserLogger = require('alife-logger');
                // Use BrowserLogger.singleton(conf) config to load the configurations specified by config.
                const __bl = BrowserLogger.singleton({
                    pid: 'your-project-id',
                        // Specify the path to which the logs are uploaded.
                        // If you want to deploy the SDK in the Singapore region, set the path to https://arms-retcode-sg.aliyuncs.com/r.png?.
                        // If you want to deploy the SDK in the US (Silicon Valley) region, set the path to http://arms-us-west-1.console.aliyun.com/r.png?.
                     uid: 'xxx', // The UID is used to identify a user. Set its value based on your businesses.
                        imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?', 
                    // Set other configurations specified by config.
                });
```

## API operation



**Note:** This method applies only to the implementation of browser monitoring by using npm.

The following table describes the parameters you can configure for `BrowserLogger.singleton(config,prePipe)`.

This method is a static method that returns a single-instance object. The loaded config and prePipe parameters take effect only when the method is called for the first time. Only generated instances are returned for subsequent calls.

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|config|Object|The site configurations. For more information about other parameters you can configure in config, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).|Yes|None|
|prePipe|Array|The content that must be reported in advance.|No|None|

This method can be used to initialize the SDK at the application entry point and obtain an instance during each call.

You can use `BrowerLogger.singleton` to obtain instances.

```
const __bl = BrowserLogger.singleton();
```

For more information about how to use other methods of `__bl`, see [API reference](/intl.en-US/Browser monitoring/API reference.md).

The configurations of config is the same as those when you use CDN to install the ARMS browser monitoring agent. For more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

If some data must be reported based on the logic of the code executed before `BrowserLogger.singleton()` is called, you must pre-report the data. For more information, see [Pre-report data]().

```
const BrowserLogger = require('alife-logger');
                // The structure of pipe is the same as the that when you use CDN to install the ARMS browser monitoring agent.
                const pipe = [
                // Report the current HTML page as an API request.
                ['api', '/index.html', true, performance.now, 'SUCCESS'], // This is equivalent to __bl.api(api, success, time, code, msg).
                // After the SDK is initialized, enable automatic Single Page Application (SPA) resolution.
                ['setConfig', {enableSPA: true}]
                ];
                const __bl = BrowserLogger.singleton({pid:'Unique site ID'},pipe);
```

## Common SDK parameters

The browser monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet more requirements. The following table describes the parameters that you can configure in the scenarios described in this topic.

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
|behavior|Boolean|Whether to record the user behavior to facilitate troubleshooting.|No|`true`|
|enableSPA|Boolean|Specifies whether to monitor the hashchange event on the page and report page view \(PV\) again. It is applicable to spa scenarios.|No|`false`|
|enableLinkTrace|Boolean|For more information about front-to-back tracing, see [t152278.md\#](/intl.en-US/Browser monitoring/Tutorials/Use the front-to-back tracing feature to diagnose causes of API errors.md).|No|`false`|

For more information about the SDK parameters that you can configure, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

**Related topics**  


[Access overview of browser monitoring](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/Access overview of browser monitoring.md)

[SDK reference](/intl.en-US/Browser monitoring/SDK reference.md)

[Install the browser monitoring probe by using CDN](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For Web applications/Install the browser monitoring probe by using CDN.md)

[Implement browser monitoring in the Weex environment](/intl.en-US/Browser monitoring/Get started with Browser Monitoring/For Weex/Implement browser monitoring in the Weex environment.md)

