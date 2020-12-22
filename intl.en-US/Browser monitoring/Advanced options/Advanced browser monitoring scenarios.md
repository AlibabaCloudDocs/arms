# Advanced browser monitoring scenarios

The browser monitoring SDK of Application Real-Time Monitoring Service \(ARMS\) provides several advanced options for browser monitoring in advanced scenarios, such as SPA page reporting, data pre-reporting, and custom performance metric reporting.

## SPA page reporting

In a single page application \(SPA\), a page will only be refreshed once. Traditionally, the page view \(PV\) data is only reported once after the page is loaded. However, PVs of sub-pages cannot be collected, and logs of other types cannot be aggregated according to sub-pages.

The ARMS browser monitoring SDK provides two methods for processing SPA pages.

-   Enable automatic SPA resolution

    This method is applicable to most SPAs that use URL hash.

    In initial configuration items, setting enableSPA to `true` can enable hashchange event listening \(triggering repeated PV reporting\) on the page and use URL hash as the page field for reporting other data.

    The <Function\>parseHash parameter can also be used together with enableSPA \(for more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md)\).

-   Manually report data

    This method is applicable to all SPA scenarios. Use this method if the first method is ineffective.

    The SDK provides the setPage method for manually updating page name during data reporting. When this method is called, page PV will be reported again by default.

    ```
    // Listen to application route change event
    app.on('routeChange', function (next) {
        __bl.setPage(next.name);
    });                    
    ```


## Pre-report data

Data reporting errors may occur in the following situations:

-   Some data needs to be reported when a page is being loaded but the SDK initialization is not complete yet \(or it is not clear if the SDK initialization is complete\).
-   The setConfig method is called in the application initialization logic. However, the loading may not be complete yet because the SDK is asynchronously loaded.

Solution: The SDK adds the `pipe` attribute to the `__bl` object to cache pre-called information into this variable. The following shows an example.

```
__bl.pipe = [
    // Report HTML of the current page as an API.
    ['api', '/index.html', true, performance.now, 'SUCCESS'],

    // After SDK initialization is complete, enable automatic SPA resolution.
    ['setConfig', {enableSPA: true}]
];            
```

To report a single data record, use:

```
__bl.pipe = ['msg', 'I'm another generic message'];          
```

The zeroth number in the array is the method name, followed by input parameters. After the SDK initialization is complete, it calls methods and parameters attached to `window.__bl.pipe` one by one.

**Note:** Before the SDK initialization is complete, if the value of `__bl.pipe` is set multiple times, the last value takes effect.

If you are not sure whether the SDK initialization is complete and do not want to add too much judgment logic, you can call `pipe` after SDK initialization is complete \(this is supported by Internet Explorer 9 and later\).

For example, in an SPA, after `autoSend: false` is set, PV is reported for the first time after application initialization. However, it is not clear if the SDK initialization is complete.

```
// Set the name of the page to 'homepage' and report PV.
__bl.pipe = ['setPage', 'homepage'];            
```

## Report custom performance metrics

You can use the `__bl.pipe` method to report the following custom performance metrics:

-   Custom First Meaningful Paint cfpt
-   Custom First Time to Interact ctti
-   Other custom performance metrics t1 - t10 \(10 metrics in total\)

The preceding custom performance metrics are reported simultaneously before the page load event is triggered.

For CDN-based access, the custom performance metrics to be reported are as follows:

```
__bl.pipe=[ 'performance',

   {
      cfpt: 100,
      ctti: 20,
      t1: 300,
      t2: 300,
      t3: 60,
      t4: 1300,
      t5: 300,
      t6: 1300,
      t7: 40,
      t8: 300,
      t9: 300,
      t10: 4100
    }];
```

For Weex access, the custom performance metrics to be reported are as follows:

```
const BrowserLogger = require('alife-logger');
// Same as the pipe structure of CDN.
const pipe = ['performance', {cfpt:100, ctti:20, t1:300, t2:300, t3:60, t4:1300, t5:300, t6:1300, t7:40, t8:300, t9:300, t10:4100}];
const __bl = BrowserLogger.singleton({pid:'Unique site ID'},pipe);
```

