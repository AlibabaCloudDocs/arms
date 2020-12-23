# Custom statistics

This topic describes the custom statistics feature provided by browser monitoring of Application Real-Time Monitoring Service \(ARMS\).

To help you monitor and collect lightweight business interaction behaviors, browser monitoring provides the following types of custom statistics:

-   Sum statistics: calculates the total number of occurrences for some events in the business, such as the number of times that a button is clicked and the number of times that a module is loaded.

-   Average statistics: calculates the average values for some events in the business, such as the average loading time of a module.


ARMS provides the following dimensions for the preceding types of custom statistics. Average statistics are used in this example.

-   Statistics details

    The statistics details line chart shows trends of the average values and the size of samples for an event within a specified period of time. Assume that the time consumption data of a module is collected. In the statistics details, you can view the average time consumption data and the size of sent samples in the corresponding period of time.

    ![statistics details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6092576751/p43703.png)

-   Geographical view

    Statistics on the event in corresponding regions are collected by province or city in China or by country or region worldwide. ARMS browser monitoring provides the reported amount, average value, and unique visitor \(UV\) data of each region. This helps the business side understand the differences between events in different regions and make decisions.

    ![geographical_view](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9626278061/p43705.png)

-   Terminal view

    Browsers, devices, operating systems, and resolutions may affect the performance, compatibility, and display of a page. ARMS browser monitoring provides the average values and sample sizes in these dimensions. This helps the business side understand the distribution of the event in different browsers, devices, operating systems, and resolutions.

    ![terminal_view](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9626278061/p43706.png)


## API method for sum statistics

After the browser monitoring SDK is introduced on the page, use the following log reporting API method in the business JavaScript file for sum statistics:

Call parameter: `__bl.sum(key, value)`

Call parameter description:

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|None|
|value|Number|The cumulative number in each report. Default value: 1.|No|1|

Example:

```
__bl.sum('event-a');
__bl.sum('event-b', 3);
```

## API method for average value statistics

After the browser monitoring SDK is introduced on the page, use the following log reporting method in the business JavaScript file for average value statistics:

Call parameter: `__bl.avg(key, value)`

Call parameter description:

|Parameter|Type|Description|Required|Default value|
|---------|----|-----------|--------|-------------|
|key|String|The name of the event.|Yes|None|
|value|Number|The number of reported items. Default value: 0.|No|0|

Example:

```
__bl.avg('event-a', 1);
__bl.avg('event-b', 3);
```

