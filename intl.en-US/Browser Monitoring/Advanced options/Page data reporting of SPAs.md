# Page data reporting of SPAs

In a single page application \(SPA\), a page is refreshed only once. Traditionally, page view \(PV\) data is reported once only after the page is loaded. However, PV data of sub-pages cannot be collected, and logs of other types cannot be aggregated based on sub-pages. This topic describes how to use Application Real-Time Monitoring Service \(ARMS\) Browser Monitoring SDK to resolve issues about page data reporting of SPAs.

ARMS Browser Monitoring SDK provides two methods for processing SPA pages.

-   Enable automatic SPA page resolution
-   Manually report data

## Enable automatic SPA page resolution

This method is applicable to most SPAs that use URL hash as the route.

In initial configuration items, set enableSPA to `true`. This way, hashchange events can be listened to on the page and PV data can be automatically reported again. URL hash is used as the page field for reporting other data.

enableSPA can also be used with parseHash. For more information, see [enableSPA](/intl.en-US/Browser Monitoring/SDK reference.mdsc_enablespa) and [parseHash](/intl.en-US/Browser Monitoring/SDK reference.md).

## Manually report data

This method is applicable to all SPAs. Use this method if the first method is ineffective.

ARMS Browser Monitoring SDK provides the setPage method for you to manually update the value of page name. You can use the new value when you report data. When this method is called, PV data will be reported again by default. For more information, see [setPage\(\)](/intl.en-US/Browser Monitoring/API reference.md).

```
// Listen to route change events of the application.
app.on('routeChange', function (next) {
    __bl.setPage(next.name);
});                    
```

**Related topics**  


[SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md)

[API reference](/intl.en-US/Browser Monitoring/API reference.md)

