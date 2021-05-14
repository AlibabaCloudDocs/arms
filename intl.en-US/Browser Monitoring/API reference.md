# API reference

The monitoring SDK provides methods that are used to report data and modify SDK configurations.

## Methods in this topic

-   Methods for data reporting: [api\(\)](#sc_api), [error\(\)](#sc_error), [sum\(\)](#sc_sum), [avg\(\)](#sc_avg), [reportBehavior\(\)](#sc_reportbehavior), and [performance\(\)](#sc_performance)
-   Methods for SDK configuration modification: [setConfig\(\)](#sc_setconfig), [setPage\(\)](#sc_setpage), and [addBehavior\(\)](#section_i3c_5cr_yvr)

## `api()`

You can call the `api()` method to report the success rate of API calls on a page.

By default, the SDK listens to JavaScript and XML \(AJAX\) requests on the page and calls this method to report data. If data on the page is requested by using JSON with Padding \(JSONP\) or other custom tools such as the client SDK, you can call the `api()` method in the data request for manual reporting.

**Note:** To call this method, we recommend you set the disabledHook to true in the SDK configurations. For more information, see [disableHook](/intl.en-US/Browser Monitoring/SDK reference.md).

Syntax of `api()` :

```
__bl.api(api, success, time, code, msg)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|api|String|The name of the method.|Yes|N/A|
|success|Boolean|Specifies whether the call is successful.|Yes|N/A|
|time|Number|The time consumed by the call.|Yes|N/A|
|code|String/Number|The response code.|No|''|
|msg|String|The response information.|No|''|

Example of `api()`:

```
var begin = Date.now(),
    url = '/data/getTodoList.json';

$.ajax({
    url: url,
    data: {id: 123456}
}).done(function (result) {
    var time = Date.now() - begin;
    // The call is successful. 
    window.__bl && __bl.api(url, true, time, result.code, result.msg);
}).fail(function (error) {
    var time = Date.now() - begin;
    // The call fails. 
    window.__bl && __bl.api(url, false, time, 'ERROR', error.message);
});            
```

[\[Back to the top\]](#sc_index)

## `error()`

You can call the `error()` method to report JavaScript \(JS\) errors or exceptions you want to capture on a page.

Generally, the SDK listens to global errors on the page and calls this method to report exceptions. However, due to the same-origin policy of the browser, error details are usually out of reach. In this case, you must manually report such errors.

Syntax of `error()`:

```
__bl.error(error, pos)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|error|Error|The JS error object.|Yes|N/A|
|pos|Object|The location where the error occurs. It contains the following three attributes.|No|N/A|
|pos.filename|String|The name of the file where the error occurs.|No|N/A|
|pos.lineno|Number|The number of the line where the error occurs.|No|N/A|
|pos.colno|Number|The number of the column where the error occurs.|No|N/A|

Example 1 of `error()`: Listen to and report JS errors on the page.

```
window.addEventListener('error', function (ex) {
    // Event parameters usually contain location information. 
    window.__bl && __bl.error(ex.error, ex);
});            
```

Example 2 of `error()`: Report a custom error.

```
window.__bl && __bl.error(new Error('A custom error occurs.'), {
    filename: 'app.js', 
    lineno: 10, 
    colno: 15
});            
```

[\[Back to the top\]](#sc_index)

## `sum()`

You can call the `sum()` method to customize the logs to be reported. The logs are used to count how many times a specific event occurs in a business scenario. You can view the following data reported by calling the `sum()` method on the Custom Statistics page:

-   The trend chart of custom events.
-   The page views \(PVs\) and unique visitors \(UVs\) of an event.
-   The dimension distribution information.

Syntax of `sum()`:

```
__bl.sum(key, value)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|N/A|
|value|Number|The number of reported items at a time.|No|1|

Example of `sum()`:

```
__bl.sum('event-a');
__bl.sum('event-b', 3);
```

[\[Back to Top\]](#sc_index)

## `avg()`

You can call the `avg()` method to customize the logs to be reported. The logs are used to count how many times a specific event occurs on average in a business scenario. You can view the following data reported by the `avg()` method on the Custom Statistics page:

-   The trend chart of custom events.
-   The PVs and UVs of an event.
-   The dimension distribution information.

Syntax of `avg()`:

```
__bl.avg(key, value)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|N/A|
|value|Number|The number of reported items.|No|0|

Example of `avg()`:

```
__bl.avg('event-a', 1);
__bl.avg('event-b', 3);
```

[\[Back to Top\]](#sc_index)

## `addBehavior()`

You can call the `addBehavior()` method to add a custom user behavior to the end of the current behavior queue.

The SDK maintains a user behavior queue with a maximum of 100 records. You can call the `addBehavior()` method to add a custom user behavior to the end of the current behavior queue. When a JS error occurs, the method reports the current behavior queue and clears the queue.

**Note:** To call this method, you must set the behavior parameter to true in the SDK configurations.

Syntax of `addBehavior()`:

```
__bl.addBehavior(behavior)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|data|Object|The behavior data. Valid values: -   name: Required. The behavior name of the STRING type. The name can be up to 20 characters in length.
-   message: Required. The behavior content of the STRING type. The value can be up to 200 characters in length.

|Yes|N/A|
|page|String|The page where the behavior happens.|No|Value of the location.pathname parameter|

Example of `addBehavior()`:

```
_bl.addBehavior({
  data:{name:'string',message:'sting'},
  page:'string'
})
```

[\[Back to Top\]](#sc_index)

## `reportBehavior()`

You can call the `reportBehavior()` method to immediately report the current behavior queue.

If you do not manually call this method, when a JS error occurs, the current behavior queue is automatically reported. The maximum size of a queue is 100. If the queue contains more than 100 behavior records, behavior records are discarded from the header of the queue.

**Note:** To call this method, you must set the behavior parameter to true in the SDK configurations.

Syntax of `reportBehavior()`:

```
__bl.reportBehavior()
```

The `reportBehavior()` method does not have request parameters.

[\[Back to Top\]](#sc_index)

## `performance()`

**Note:** This method is applicable only to web clients.

After the onLoad method is called, the `performance()` method is called to report custom performance metrics other than the default performance metrics.

**Note:** You must call this method after the onLoad method is called. Otherwise, the call fails because the collection of default performance metrics is incomplete. The performance\(\) method can be called only once during each PV.

Usage of `performance()`:

1.  Set the autoSendPerf parameter to false to disable automatic reporting of performance metrics and wait for manual reporting.
2.  Call the `__bl.performance(Object)` method to manually report custom performance metrics. In this process, the default performance metrics are automatically reported.

Example 1 of `performance()` \(by using CDN\):

```
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …});
  }, 1000); // Set a delay to ensure that the default performance data is collected. 
};
```

Example 2 of `performance()` \(by using npm packages\):

```
const BrowserLogger = require('alife-logger');
const __bl = BrowserLogger.singleton({pid:'Unique site ID'});
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …});
  }, 1000); // Set a delay to ensure that the default performance data is collected. 
};
```

**Note:** Descriptions of custom performance metrics:

-   cfpt: the custom first paint time
-   ctti: the first custom time to interact
-   t1 to t10: ten custom performance metrics

[\[Back to Top\]](#sc_index)

## `setConfig()`

You can call the `setConfig()` method to modify specific configuration items after the SDK initialization. For more information, see [SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md).

Syntax of `setConfig()`:

```
__bl.setConfig(next)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|next|Object|The configuration item and its value that you want to modify.|Yes|N/A|

Example of `setConfig()`: Modify the value of the disableHook parameter to disable automatic API reporting.

```
__bl.setConfig({
    disableHook: true
});            
```

[\[Back to the top\]](#sc_index)

## `setPage()`

You can call the `setPage()` method to reset the page name of a page. PV data is reported again by default. This method is typically used for single-page applications \(SPAs\). For more information, see [Page data reporting of SPAs](/intl.en-US/Browser Monitoring/Advanced options/Page data reporting of SPAs.md).

Syntax of `setPage()`:

```
__bl.setPage(page, sendPv)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|page|String|The new page name.|Yes|N/A|
|sendPv|Boolean|Specifies whether to report PV data. PV data is reported by default.|No|`true`|

Example 1 of `setPage()`: Set the name of the current page to the current URL hash, and report PV data again.

```
__bl.setPage(location.hash);            
```

Example 2 of `setPage()`: Set the name of the current page to 'homepage' without triggering PV data reporting.

```
__bl.setPage('homepage', false);     
```

[\[Back to Top\]](#sc_index)

## FAQ

Q: What do I do if I am not sure whether the SDK has been loaded when I call the `__bl.performance()` method?

A: For more information, see [t152282.md\#section\_nsg\_w5u\_r05](/intl.en-US/Browser Monitoring/Advanced options/Page data reporting of SPAs.mdsection_nsg_w5u_r05).

[\[Back to Top\]](#sc_index)

**Related topics**  


[SDK reference](/intl.en-US/Browser Monitoring/SDK reference.md)

[Page data reporting of SPAs](/intl.en-US/Browser Monitoring/Advanced options/Page data reporting of SPAs.md)

