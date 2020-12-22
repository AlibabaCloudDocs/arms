# Implement browser monitoring in the Weex environment

This topic describes how to implement the browser monitoring feature of Application Real-Time Monitoring Service \(ARMS\) in the Weex environment.

## Import the NPM package

To use the browser monitoring feature of ARMS in the Weex environment, run the following command in your project to import the Node Package Manager \(npm\) package named alife-logger and use the dedicated WeexLogger module to report logs:

```
npm install alife-logger --save
```

## Initialize the SDK

Create the monitor.js file in the /utils directory and initialize the SDK based on the following sample code.

**Note:** To call the singleton\(props\) method at the entry point of a Weex application to obtain instances, configure parameters for the imported props. For more information, see the following sections:

-   [General method: @static singleton\(\)](#section_mof_zn6_n9l)
-   [General method: setPage\(\)](#section_a9k_j3s_i38)
-   [General method: setConfig\(\)](#section_t5p_nqr_kn6)

```
// Add the following content to monitor.js:
import WeexLogger from 'alife-logger/weex';

const fetch = weex.requireModule('stream').fetch;
const serialize = (data) = >{
    data = data || {};
    var arr = [];
    for (var k in data) {
        if (Object.prototype.hasOwnProperty.call(data, k) && data[k] ! == undefined) {
            arr.push(k + '=' + encodeURIComponent(data[k]).replace(/\(/g, '%28').replace(/\)/g, '%29'));
        }
    }
    return arr.join('&');
}

// Initialize the SDK.
const wxLogger = WeexLogger.singleton({
    pid: 'your-project-id',
    uid: 'zhangsan',
    // Configure the UID to generate unique visitor (UV) reports.
    page: 'Lazada | Home',
    // Configure the name of the initial page. The SDK sends page view (PV) reports after the initialization is complete.
    imgUrl: 'https://arms-retcode.aliyuncs.com/r.png?',
    // Specify the path to which the reports are sent. If you want to deploy the SDK in the Singapore region, set the path to 'https://arms-retcode-sg.aliyuncs.com/r.png?'.
    // The following code provides an example on how to use the GET method to send reports:
    sendRequest: (data, imgUrl) = >{
        const url = imgUrl + serialize(data);
        fetch({
            method: 'GET',
            url
        });
    },
    // The following code provides an example on how to use the POST method to send reports:
    postRequest: (data, imgUrl) = >{
        fetch({
            method: 'POST',
            type: 'json',
            url: imgUrl,
            body: JSON.stringify(data)
        });
    }
});

export
default wxLogger;
```

## Report logs

Call the corresponding methods to report logs based on instances.

```
// in some biz module
import wxLogger from '/utils/monitor';
wxLogger.api('/search.do', true, 233, 'SUCCESS');
```

## General method: @static singleton\(\)

@static singleton\(\) is a static method used to return a single instance. props takes effect only when the method is called for the first time. The following table describes the parameters you can configure when you call the method.

This method can be used to initialize the SDK at the application entry point. For more information, see [Initialize the SDK](#initialization).

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|pid|String|The site ID.|Yes|None|
|page|String|The page name after initialization.|No|None|
|uid|String|The ID of the user.|Yes|None|
|imgUrl|String|The path to which the logs are uploaded. The path ends with a question mark \(?\).|No|None|

## General method: setPage\(\)

setPage\(\) is used to set the name of the current page and report the PV logs once by default.

```
import wxLogger from '/utils/monitor';
// ...
wxLogger.setPage(nextPage);
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|nextPage|String|Page Name|Yes|None|

## General method: setConfig\(\)

setConfig\(\) is used to modify configurations after the SDK is initialized. The configuration method is the same as that of singleton\(\). For more information about the parameters that you can configure for the method, see [setConfig\(\)](/intl.en-US/Browser monitoring/API reference.md).

```
import wxLogger from '/utils/monitor';
// ...
wxLogger.setConfig(config);
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|config|Object|The configuration items you want to modify.|Yes|None|
|uid|String|The user ID used to collect the unique visitor \(UV\) data.|Yes|Storage settings|

## Log reporting methods

For more information, see the log reporting methods in [API reference](/intl.en-US/Browser monitoring/API reference.md).

## Common SDK parameters

The browser monitoring feature of ARMS allows you to configure a variety of SDK parameters to meet more requirements. The following table describes the parameters that you can configure in the scenarios described in this topic.

|Parameter|Type|Description|Required|Default Value|
|---------|----|-----------|--------|-------------|
|pid|String|The unique ID of the project, which is automatically generated when ARMS creates the site.|Yes|No default value|
|uid|String|The user ID, which is used to identify the user. You can manually configure the ID to search for the user based on the user ID. If this parameter is not configured, the updates are automatically generated by the SDK and updated every six months.|Yes|No default value|
|tag|String|The input tag. Each log carries a tag.|No|No default value|
|release|String|The version of the application. We recommend that you configure to view the reports of different versions.|No|`undefined`|
|environment|String|The production environment. Valid values: prod, gray, pre, daily, and local. -   prod indicates the online environment.
-   gray indicates the grayscale environment.
-   pre: the staging environment.
-   daily indicates the daily environment.
-   local indicates the local environment.

|No|`prod`|
|sample|Integer|The sampling configuration of the log. The value ranges from 1 to 100. Sample Performance logs and successful API logs in accordance with the `1/sample` ratio. For more information about the metrics of performance logs and successful API logs, see [Statistical metrics](/intl.en-US/Browser monitoring/Statistical metrics.md).|No|`1`|

For more information about the SDK parameters that you can configure, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

