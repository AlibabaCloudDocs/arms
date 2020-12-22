# Overview

The browser monitoring function of Application Real-Time Monitoring Service \(ARMS\) monitors experience data for Web pages, including the page loading speed \(speed test\), page stability \(JS errors\), and external service calling success rate \(API\), to check the healthiness of Web pages.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4882576751/p43324.png)

In addition, based on the Application Performance Index \([APDEX](http://www.apdex.org/)\) algorithm, ARMS calculates the satisfaction rating of application sites and pages, allowing you to learn user experience on the sites and pages.

## Why is browser monitoring necessary?

When a user accesses a service, the whole process can be divided into three phases: page production time \(server status\), page load time, and page run time.

To make sure stable online services, the running status of services is monitored on the server. Currently, the server monitoring system is quite mature, but the monitoring of page load time and run time is far from satisfactory. For example:

-   You cannot capture the access errors of users immediately.
-   You do not know the actual response time for users from different countries or regions to access your website.
-   You have no idea about the performance and success rate of asynchronous data calls of each application.

## Solution

The ARMS browser monitoring platform monitors the status of page load time and run time, and reports data, such as the page load performance, runtime exceptions, and API call status and consumed time, to the logger. Then, the platform monitors the access of all real online users based on the rich real-time log analysis and processing services provided by ARMS. Finally, the platform displays results on reports to help you detect and diagnose problems promptly.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4882576751/p43325.png)

## Browser and platform compatibility

|Browser/Platform|Supported version|Automatic reporting|Active reporting|
|----------------|-----------------|-------------------|----------------|
|Safari|Safari 9+|✔️|✔️|
|Google Chrome|Google Chrome 49+|✔️|✔️|
|Internet Explorer|IE 9+|✔️|✔️|
|Microsoft Edge|Microsoft Edge 12+|✔️|✔️|
|Firefox|Firefox 36+|✔️|✔️|
|Opera|Opera 43+|✔️|✔️|
|Safari for iOS|Safari for iOS 9.2+|✔️|✔️|
|Android browser|android\_webkit 4.4.2+|✔️|✔️|
|Weex|Weex 0.16.0+|✔️|

