---
keyword: [APM, browser monitoring, page performance, page health, access speed, api monitoring]
---

# What is ARMS Browser Monitoring?

Browser Monitoring of Application Real-Time Monitoring Service \(ARMS\) is applicable to scenarios such as web page monitoring, Weex monitoring, and mini-program monitoring. You can monitor web pages and mini-programs based on the following metrics: the page loading speed \(speed test\), page stability \(JavaScript errors\), and success rate of calls to external services that are APIs.

## Why is Browser Monitoring necessary?

When a user accesses a service, the whole process can be divided into three phases: page generation \(server status\), page loading, and page runtime.

To ensure stable online services, the server monitors the status of these services. Existing server monitoring systems are quite mature, but the monitoring of page loading and runtime is far from satisfactory. For example:

-   You cannot immediately capture the errors that users encounter when they access your website.
-   You do not know the actual response time for users from different countries or regions to access your website.
-   You have no idea about the performance and success rate of asynchronous data calls of each application.

## Solution

ARMS Browser Monitoring monitors the status of page loading and runtime, and reports data to the logger. The data includes the page load performance, runtime exceptions, and API call status and consumed time. Then, the platform monitors the access of all real online users based on the rich real-time log analytics and processing services provided by ARMS. Finally, the platform presents visual reports to help you detect and diagnose problems at the earliest opportunity.

![Web page monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6968342161/p75797.png)

## Scenarios

ARMS Browser Monitoring supports the following scenarios:

-   Web/H5
    -   [Install the browser monitoring probe by using CDN](/intl.en-US/Browser monitoring/Quick start/For Web applications/Install the browser monitoring probe by using CDN.md)
    -   [Implement browser monitoring by using npm](/intl.en-US/Browser monitoring/Quick start/For Web applications/Implement browser monitoring by using npm.md)
-   Weex

    [Implement browser monitoring in the Weex environment](/intl.en-US/Browser monitoring/Quick start/For Weex/Implement browser monitoring in the Weex environment.md)

-   Mini-programs
    -   [Monitor DingTalk mini programs](/intl.en-US/Browser monitoring/Quick start/For mini programs/Monitor DingTalk mini programs.md)
    -   [Monitor Alipay mini programs](/intl.en-US/Browser monitoring/Quick start/For mini programs/Monitor Alipay mini programs.md)
    -   [Monitor WeChat mini programs](/intl.en-US/Browser monitoring/Quick start/For mini programs/Monitor WeChat mini programs.md)
    -   [Monitor other mini programs](/intl.en-US/Browser monitoring/Quick start/For mini programs/Monitor other mini programs.md)

## Capabilities

ARMS Browser Monitoring provides the following capabilities:

-   [Page speed](/intl.en-US/Browser monitoring/Tutorials/Diagnose slow page loading by using ARMS Browser Monitoring.md)
-   [JS errors](/intl.en-US/Browser monitoring/Tutorials/Diagnose JS errors by using ARMS browser monitoring.md)
-   [API request](/intl.en-US/Browser monitoring/Console functions/API request.md)
-   [Front-to-back tracking](/intl.en-US/Browser monitoring/Tutorials/Use the front-to-back tracing feature to diagnose causes of API errors.md)

## Browser and platform compatibility

|Browser or platform|Supported version|Automatic report by the SDK|Manual report|
|-------------------|-----------------|---------------------------|-------------|
|Safari|Safari 9+|✔️|✔️|
|Chrome|Chrome 49+|✔️|✔️|
|IE|IE 9+|✔️|✔️|
|Edge|Edge 12+|✔️|✔️|
|Firefox|Firefox 36+|✔️|✔️|
|Opera|Opera 43+|✔️|✔️|
|Safari for iOS|Safari for iOS 9.2+|✔️|✔️|
|Android Browser|android\_webkit 4.4.2+|✔️|✔️|
|Weex|Weex 0.16.0+|✖️|✔️|

