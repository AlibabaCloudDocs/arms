---
keyword: [Browser Monitoring, Pre-report, Pipe]
---

# Pre-report data

Data reporting may fail in specific cases, for example, when the software development kit \(SDK\) initialization has not been completed. This topic describes how to use the SDK of Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring to pre-report data.

## Data reporting failure scenarios

Data reporting errors may occur in the following scenarios:

-   Some data needs to be reported when a page is being loaded but the SDK initialization is not complete or it is not clear if the SDK initialization is complete.
-   The setConfig method is called in the application initialization logic. However, the loading may not be complete because the SDK is asynchronously loaded.

## Solution

The SDK adds the pipe attribute to the `__bl` object to cache pre-called information into this variable. Example:

```
__bl.pipe = [
    // Report HTML of the current page as an API.
    ['api', '/index.html', true, performance.now, 'SUCCESS'], // This is equivalent to __bl.api(api, success, time, code, msg).

    // After SDK initialization is complete, enable automatic Single Page Application (SPA) resolution.
    ['setConfig', {enableSPA: true}]
];            
```

To report a single data record, use:

```
__bl.pipe = ['msg', 'I'm another generic message'];          
```

The zeroth number in the array is the method name, followed by input parameters. After the SDK initialization is complete, it calls methods and parameters attached to `window.__bl.pipe` one by one.

**Note:** Before the SDK initialization is complete, if the value of `__bl.pipe` is set multiple times, the last value that is set takes effect.

If you are not sure whether the SDK initialization is complete and do not want to add too much judgment logic, you can call pipe after SDK initialization is complete \(this is supported by Internet Explorer 9 and later\).

For example, in an SPA, after `autoSend: false` is set, page view \(PV\) is reported for the first time after application initialization. However, it is not clear if the SDK initialization is complete.

```
// Set the name of the page to 'homepage' and report PV.
__bl.pipe = ['setPage', 'homepage'];            
```

**Related topics**  


[SDK reference](/intl.en-US/Browser monitoring/SDK reference.md)

[API reference](/intl.en-US/Browser monitoring/API reference.md)

