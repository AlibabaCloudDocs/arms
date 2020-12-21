# External call

You can use the external call feature of Application Real-Time Monitoring Service \(ARMS\) application monitoring to locate slow calls or errors during the external calls of an application.

## Procedure

1.  In the left-side navigation pane, choose **Application Monitoring** \> **Applications**. In the top navigation bar, select a region.

2.  On the Applications page, click the name of the application you want to monitor.

3.  In the left-side navigation pane, click **External Calls**.

    All external calls of the application are listed on the left of the External Calls page. You can sort the calls by response time, request count, error count, or exception count.


## Overview

You can click an external call in the left-side call list to view the request count, response time, error count, and HTTP status code of the external call on the Overview tab.

![External call overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3394658061/p185227.png)

## Call source

You can click an external call in the left-side call list to view the request count, response time, and error count of all interfaces related to the external call on the Call Source tab.

![pg_am_external_calls](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3394658061/p82848.png)

You can perform the following operations on the Call Source tab:

-   Click **Collapse/Expand All** to collapse or expand all interfaces.
-   Enter the keyword of an application name or an interface \(span\) name in the search box on the top of the tab, and then click the search icon to filter out the interfaces that meet the conditions specified by the keyword.
-   Click the collapse panel where the interface information is located, or click the up or down arrow at the end of the row to expand or collapse the performance metric information of this interface.

## Interface snapshot

You can click an external call in the left-side call list to view the parameters of the call on the Interface Snapshot tab.

