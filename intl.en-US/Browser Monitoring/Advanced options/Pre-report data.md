---
keyword: [frontend monitoring, pre-report data, pipe]
---

# Pre-report data

Data reporting may fail in specific cases, such as when the SDK initialization is not complete. This topic describes how to use the SDK of Application Real-Time Monitoring Service \(ARMS\) frontend monitoring to pre-report data.

## Scenarios in which data reporting failures occur

Data reporting failures may occur in the following scenarios:

-   Some data needs to be reported when a page is being loaded but the SDK initialization is not complete or the initialization result cannot be determined.
-   The setConfig method is called in the application initialization logic. However, the loading may not be complete because the SDK is asynchronously loaded.

## Solution

The SDK adds the pipe attribute to the `__bl` object to cache the pre-called information into the \_\_bl.pipe variable. The following code provides an example:

```
__bl.pipe = [
    // Report the current HTML page as an API request. 
    ['api', '/index.html', true, performance.now, 'SUCCESS'], // This is equivalent to __bl.api(api, success, time, code, msg). 

    // After the SDK is initialized, enable automatic single-page application (SPA) resolution. 
    ['setConfig', {enableSPA: true}]
];            
```

To report a single data record, run the following command:

```
__bl.pipe = ['msg', 'I'm another generic message'];          
```

The zeroth number in the array is the method name, followed by input parameters. After the SDK initialization is complete, the SDK calls methods and parameters that are attached to `window.__bl.pipe` one by one.

**Note:** Before the SDK initialization is complete, if the value of the `__bl.pipe` parameter is set multiple times, the last value that is set takes effect.

If you are not sure whether the SDK initialization is complete and do not want to add too much judgment logic, you can call the pipe method after the SDK is initialized. This is supported by Internet Explorer 9 and later.

For example, in an SPA, after you specify `autoSend: false`, page view \(PV\) data is reported for the first time after the application initialization. However, whether the initialization is complete cannot be determined.

```
// Set the name of the page to homepage and report the PV data. 
__bl.pipe = ['setPage', 'homepage'];            
```

**Related topics**  


[SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md)

[API reference](/intl.en-US/Browser Monitoring/API reference.md)

