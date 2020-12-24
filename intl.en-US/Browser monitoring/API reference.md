# API reference

The monitoring SDK provides API operations such as data reporting operations and method operations that are used to modify SDK configurations.

## Operations in this topic

-   Data reporting operations: [api\(\)](#sc_api) \| [error\(\)](#sc_error) \| [sum\(\)](#sc_sum) \| [avg\(\)](#sc_avg) \| [reportBehavior\(\)](#sc_reportbehavior) \| [performance\(\)](#sc_performance)
-   Method operations: [setConfig\(\)](#sc_setconfig) \| [setPage\(\)](#sc_setpage) \| [addBehavior\(\)](#section_i3c_5cr_yvr)

## api\(\)

You can call the api\(\) operation to report the success rate of API calls on the page.

By default, the SDK listens for AJAX requests on the page and calls this operation to report. If data on the page is requested by using JSONP or other custom methods such as the client SDK, you can call api\(\) in the data request method for manual reporting.

**Note:** To call this operation, we recommend you set disabledHook to true in SDK configuration items. For more information, see [disableHook](/intl.en-US/Browser monitoring/SDK reference.md).

api\(\) syntax:

```
__bl.api(api, success, time, code, msg)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|api|String|The name of the operation.|Yes|None|
|success|Boolean|Specifies whether the call is successful.|Yes|None|
|time|Number|The time consumed by the operation call.|Yes|None|
|code|String/Number|The returned code.|No|''|
|msg|String|The response information.|No|''|

Example of api\(\)

```
var begin = Date.now(),
    url = '/data/getTodoList.json';

$.ajax({
    url: url,
    data: {id: 123456}
}).done(function (result) {
    var time = Date.now() - begin;
    // Reports that the operation call is successful.
    window.__bl && __bl.api(url, true, time, result.code, result.msg);
    // do something ....
}).fail(function (error) {
    var time = Date.now() - begin;
    // Reports that the operation call fails.
    window.__bl && __bl.api(url, false, time, 'ERROR', error.message);
    // do something ...
});            
```

[\[Back to the top\]](#sc_index)

## error\(\)

You can call the error\(\) operation to report JavaScript \(JS\) errors or exceptions you want to capture on the page.

Generally, the SDK listens for global errors on the page and calls this operation to report exceptions. However, due to the same-origin policy of the browser, error details are usually out of reach. In this case, you must manually report such errors.

error\(\) syntax:

```
__bl.error(error, pos)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|error|Error|The JS error object.|Yes|None|
|pos|Object|The location where the error occurs. It contains the following three attributes.|No|None|
|pos.filename|String|The name of the file where the error occurs.|No|None|
|pos.lineno|Number|The number of the row where the error occurs.|No|None|
|pos.colno|Number|The number of the column where the error occurs.|No|None|

Example 1 of error\(\): Listen to and report JS errors on the page.

```
window.addEventListener('error', function (ex) {
    // Event parameters usually contain position information.
    window.__bl && __bl.error(ex.error, ex);
});            
```

Example 2 of error\(\): Report a custom error.

```
window.__bl && __bl.error(new Error('A custom error occurs.'), {
    filename: 'app.js', 
    lineno: 10, 
    colno: 15
});            
```

[\[Back to the top\]](#sc_index)

## sum\(\)

You can call the sum\(\) operation to customize the reported logs. The logs are used to count how many times a specific business event occurs. You can view the following data reported by sum\(\) on the Custom Statistics page:

-   The trend graph of the custom events.
-   The page views \(PVs\) and unique visitors \(UVs\) of an event.
-   The dimension distribution information.

sum\(\) syntax:

```
__bl.sum(key, value)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|None|
|value|Number|The number of reports at a time.|No|1|

Example of sum\(\):

```
__bl.sum('event-a');
__bl.sum('event-b', 3);
```

[\[Back to the top\]](#sc_index)

## avg\(\)

You can call the avg\(\) operation to customize the reported logs. The logs are used to count how many times a specific event occurs on average in a business scenario. You can view the following data reported by avg\(\) on the Custom Statistics page:

-   The trend graph of the custom events.
-   The PVs and UVs of an event.
-   The dimension distribution information.

avg\(\) syntax:

```
__bl.avg(key, value)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|None|
|value|Number|The number of reported items.|No|0|

Example of avg\(\):

```
__bl.avg('event-a', 1);
__bl.avg('event-b', 3);
```

[\[Back to the top\]](#sc_index)

## addBehavior\(\)

You can call the addBehavior\(\) operation to add a custom user behavior to the end of the current behavior queue.

The SDK maintains a user behavior queue with a maximum of 100 records. You can call the addBehavior\(\) operation to add a custom user behavior to the end of the current behavior queue. When a JS error occurs, the operation reports the current behavior queue and clears the queue.

**Note:** To call this operation, you must set behavior to true in SDK configuration.

addBehavior\(\) syntax:

```
__bl.addBehavior(behavior)
```

|Parameter|Type|Description|Required|Default value|
|data|Object|The behavior data. Valid values: -   name: the behavior name of the string type. The name can be up to 20 characters in length. This parameter is required.
-   message: the behavior content of the string type. The value can be up to 200 characters in length. This parameter is required.

|Yes|None|
|page|String|The page where the behavior happens.|No|Value of location.pathname|

Example of addBehavior\(\):

```
_bl.addBehavior({
  data:{name:'string',message:'sting'},
  page:'string'
})
```

[\[Back to the top\]](#sc_index)

## reportBehavior\(\)

You can call the reportBehavior\(\) operation to report the current behavior queue immediately.

If you do not manually call this method, when a JS error occurs, the current behavior queue is automatically reported. The maximum size of a queue is 100. If the queue contains more than 100 behavior records, behavior records are discarded from the header of the queue.

**Note:** To call this operation, you must set behavior to true in SDK configuration.

reportBehavior\(\) syntax:

```
__bl.reportBehavior()
```

reportBehavior\(\) does not have request parameters.

[\[Back to the top\]](#sc_index)

## performance\(\)

**Note:** This operation is applicable only to web clients.

After the onLoad operation is performed, performance\(\) is called to report custom performance metrics other than the default performance metrics.

**Note:** You must call this operation after the onLoad operation is performed. Otherwise, the call fails because the collection of default performance metrics is incomplete. The operation can be called only once during each PV.

Usage of performance\(\):

1.  Set the SDK configuration item autoSendPerf to false to disable automatic reporting of performance metrics and wait for manual reporting.
2.  Call the \_\_bl.performance\(Object\) method to manually report custom performance metrics. In this process, the default performance metrics are automatically reported.

Example 1 of performance\(\) \(accessed by using CDN\):

```
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …}) ;
  }, 1000); // Set a delay to ensure that the default performance data is collected.
};
```

Example 2 of performance\(\) \(accessed by using npm packages\):

```
const BrowserLogger = require('alife-logger');
const __bl = BrowserLogger.singleton({pid:'Unique site ID'});
window.onload = () => {
  setTimeout(()=>{
    __bl.performance({cfpt:100, ctti:200, t1:300, …}) ;
  }, 1000); // Set a delay to ensure that the default performance data is collected.
};
```

**Note:** Descriptions of custom performance metrics:

-   cfpt: the custom first paint time
-   ctti: the first custom time to interact
-   t1 to t10: ten custom performance metrics

[\[Back to the top\]](#sc_index)

## setConfig\(\)

You can call the setConfig\(\) operation to modify some configuration items after SDK initialization. For more information, see [SDK reference](/intl.en-US/Browser monitoring/SDK reference.md).

setConfig\(\) syntax:

```
__bl.setConfig(next)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|next|Object|The configuration items to be modified and their values.|Yes|None|

Example of setConfig\(\): Modify the disableHook value to disable automatic API reporting.

```
__bl.setConfig({
    disableHook: true,
    setUserGroup:function () {
        return 'YourUserGroup'
    }
});            
```

[\[Back to the top\]](#sc_index)

## setPage\(\)

You can call the setPage\(\) operation to reset the page name of a page. PV is reported again by default. This method is typically used for single-page applications. For more information, see [t152282.md\#](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md).

setPage\(\) syntax:

```
__bl.setPage(page, sendPv)
```

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|page|String|The new page name.|Yes|None|
|sendPv|Boolean|Specifies whether to report PV. PV is reported by default.|No|`true`|

Example 1 of setPage\(\): Set the name of the current page to the current URL hash, and report PV again.

```
__bl.setPage(location.hash);            
```

Example 2 of setPage\(\): Set the name of the current page to 'homepage' without triggering PV reporting.

```
__bl.setPage('homepage', false);     
```

[\[Back to the top\]](#sc_index)

## FAQ

Q: What do I do if I am not sure whether the SDK has been loaded when I call the \_\_bl.performance\(\) operation?

A: For more information, see [t152282.md\#section\_nsg\_w5u\_r05](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.mdsection_nsg_w5u_r05).

[\[Back to the top\]](#sc_index)

**Related topics**  


[SDK reference](/intl.en-US/Browser monitoring/SDK reference.md)

[t152282.md\#](/intl.en-US/Browser monitoring/Advanced options/Advanced browser monitoring scenarios.md)

