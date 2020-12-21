# Java application monitoring and diagnosis solution

In this scenario, the application monitoring solution based on Application Real-Time Monitoring Service \(ARMS\) is used to resolve pain points in monitoring distributed Java applications.

The rapid growth of Internet businesses has produced increasing traffic pressure and more complicated business logic. As a result, traditional single-machine applications can no longer meet the business requirements of enterprises. An increasing number of websites has used the distributed deployment architecture. The basic development frameworks, such as Spring Cloud and Dubbo, is becoming mature. More enterprises have vertically split their website architectures by business module and used the microservice architecture. The microservice architecture is more suitable for collaborative development and fast iterations.

The distributed microservice architecture has advantages in terms of development efficiency. However, this architecture poses huge challenges on traditional monitoring, O&M, and diagnosis technologies. For example, when the distributed microservice architecture was implemented on Taobao \(www.taobao.com\), Alibaba encountered the following challenges:

-   Difficulty in locating issues

    The customer service team submits the purchase issues of consumers to the technical support for troubleshooting. A website request in the distributed microservice architecture passes through multiple services and nodes before a result is returned. If an error occurs, the O&M engineers must check the logs on multiple servers to identify the error cause. In most cases, multiple teams must be work together to troubleshoot a simple issue.

-   Difficulty in identifying bottlenecks

    When a website fails to respond to access requests, the O&M engineers cannot identify the bottleneck. This is because the bottleneck can be a network issue between the user terminal and the server, server overloading, or database overloading. Even if the cause is identified, the error in the code is still difficult to identify.

-   Difficulty in identifying the architecture

    The business logic has become more complicated. The downstream services \(databases, HTTP APIs, or caches\) on which an application depends are difficult to identify based on the code. The external calls that depend on the application are also difficult to identify based on the code. In addition, business logic identification, architecture governance, and capacity planning become more difficult for enterprises. For example, when enterprises prepare for Double 11 promotion campaigns, the number of servers required for each application is difficult to predict.


## ARMS-based application monitoring solution

ARMS provides the **application monitoring** feature based on the distributed tracing and monitoring system named EagleEye. This feature helps website developers and operators resolve the preceding issues without the need to modify the existing code.

**View the call topology**

You can view the call topology of an application on ARMS, for example, services that depend on the application and downstream services on which the application depends. In the following figure, a bottleneck occurs when an unknown application calls the monitored application. The average consumed time is more than 3,000 ms.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1360537751/p43318.png)

**Reports of slow services and slow SQL statements**

You can go to the SQL analysis report of an application to locate the slow SQL statements and slow services.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1360537751/p42273.png)

**Query distributed trace**

You can click the interface snapshot of a slow SQL statement. Then, you can find a request that includes the SQL call, view the call stack of the method, and then identify the code of the issue.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2360537751/p43319.png)

Either from the global perspective or from a single call, ARMS provides a comprehensive solution to address your pain points in distributed Java application monitoring. You can integrate application monitoring with browser monitoring and business transaction. ARMS provides all-around protection for your sites from critical business metrics and user experience to application performance.

