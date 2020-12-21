Overview 
=============================

The business transaction feature provided by ARMS allows you to visually define business requests in a way that is non-intrusive to existing code. This feature provides abundant business-specific performance metrics and diagnostic capabilities.

Benefits 
-----------------------------

Traditional monitoring tools measure application health status from perspectives such as infrastructures, application systems, and requests. However, these perspectives lack business semantics and cannot reflect business metrics such as average response time or success rate of order placement in the current day.

The business transaction feature can measure application performance and stability from the business perspective, which provides comprehensive monitoring of key business transactions. The business transaction feature tracks and collects business information of an application and presents business metrics such as response time, frequency, and error rate on a timely basis. This can resolve the issue of mappings between applications and business performance.

The following table lists the benefits of the business transaction feature compared with monitoring based on business logs or online analytical processing (OLAP).


|             Monitoring method             |                                                                        Access cost                                                                         |                                              Timeliness                                              |                                   Flexibility                                    |
|-------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| Business transaction (application agents) | Low. Business information is automatically collected and reported in applications.                                                                         | Real-time. Data is aggregated and computed in the background and displayed on a timely basis.        | High. Mapping rules are configured flexibly and take effect immediately.         |
| Custom monitoring (logs)                  | High. You must modify the application to display business information in the logs.                                                                         | Real-time.                                                                                           | Low. You must modify the logs before you can obtain the results of new analysis. |
| Traditional OLAP/BI tools                 | High. You must create offline analysis databases to avoid affecting the performance of your online services. Data must be synchronized on a regular basis. | Not real-time. Data cannot be analyzed in real time due to intervals caused by data synchronization. | Medium. This metric depends on the integrity of the business data.               |



Visual definition of business requests in a non-intrusive way 
----------------------------------------------------------------------------------

Typically, business information such as the order amount, username, user attributes, business operations, and source is contained in the headers, request parameters, and sessions of HTTP requests or in the request parameters of RPC APIs. The business transaction feature allows you to collect the business information in real time by using Java agents and reports the information together with the corresponding URLs and API names.

You can click Scenario-based Traces in the ARMS console and define the mappings between specific business information and URLs or RPC APIs in the graphical interface to correlate business with service calls. The mappings include the information to be matched and the dimensions on which information is split.

![Custom business transaction rules](../images/p111631.png)

The preceding figure illustrates how the transaction order creation business is configured based on the following rules:

* Select Start equal from the Service name drop-down list and start the service name with `/api`.

* Select Header from the Filter rules drop-down list, enter **action** as the key value, and then set the threshold to **order** .

* Select Parameter from the Grouping Rules drop-down list and enter **name** as the key value.




Abundant business-specific performance metrics and diagnostic capabilities 
-----------------------------------------------------------------------------------------------

On the Business monitoring details page, you can view the business topology and three key metrics of the business, including the throughput, response time, and error rate. You can also correlate the business with the corresponding database requests, exceptions, and traces at all levels.

![Business scenario traces](../images/p111634.png)

The preceding figure shows the application topology of the transaction order creation business, and metrics such as the request volumes of different products, response time, and errors.

Request for trial 
--------------------------------------

ARMS provides a 15-day free trial edition. After you activate the service, you can use features such as scenario-based tracing, application monitoring, browser monitoring, and Prometheus monitoring. You can click [here](https://common-buy.aliyun.com/?commodityCode=arms#/open) to activate the trial.
**Note** Scan the following QR code to join the DingTalk group.
![dg__business_dingding](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7037258061/p92785.png)
