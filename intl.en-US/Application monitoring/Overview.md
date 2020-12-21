# Overview

Application Real-Time Monitoring Service \(ARMS\) is an application performance management \(APM\) service. To monitor an application, you only need to install the ARMS agent. You do not need to modify the code of the application. The ARMS agent helps you identify abnormal and slow API operations, view request parameters, and detect system bottlenecks. This improves the efficiency of online troubleshooting.

## Automatically discover the application topology

The ARMS agent can automatically identify the upstream and downstream dependencies of applications. The ARMS agent can capture, compute, and display the traces that are formed by different applications in a remote procedure call \(RPC\) framework, such as Dubbo, HTTP, and HSF. You can identify performance bottlenecks and abnormal calls in the system by using the application topology.

## View the 3D topology

A 3D topology shows the health status of applications, services, and hosts. It also shows the upstream and downstream dependencies. The 3D topology helps you detect abnormal services, affected applications, and related hosts. You can then identify the causes of issues, perform troubleshooting, and resume services in a timely manner.

## Capture abnormal and slow transactions

You can obtain the stack analysis reports of slow SQL queries, accumulated Message Queue \(MQ\) messages, or exceptions, and conduct more detailed analysis.

## Automatically discover and monitor API requests

ARMS can automatically discover and monitor common web frameworks and RPC frameworks in application code. ARMS can also automatically collect statistics on metrics such as the number of calls, response time, and number of abnormal web API requests and RPC API requests.

## Perform real-time diagnosis

If you need to monitor the application performance for a short period of time, for example, when you release an application or perform stress tests on the application, you can use the real-time diagnosis feature. After real-time diagnosis is enabled for an application, ARMS monitors the application for 5 minutes and reports all the trace data that is generated during this period. If an error occurs on a trace, you can use call stack waterfall charts and the thread profiling feature to identify the cause of the error.

## Perform multi-dimensional troubleshooting

You can view the details of distributed and local call stacks, and perform analysis based on multiple dimensions, such as application, IP address, and time consumption. You can also use the comprehensive troubleshooting feature of ARMS custom monitoring to troubleshoot transactions and tickets.

## Integrate with the Alibaba Cloud PaaS platform

ARMS application monitoring can be integrated with the Alibaba Cloud PaaS platform named [Enterprise Distributed Application Service \(EDAS\)](https://www.alibabacloud.com/zh/product/edas). You can monitor applications that run on EDAS with improved efficiency.

![Integrate with EDAS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0294122951/p42286.png)

