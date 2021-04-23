# Pricing of Prometheus Service

Two editions of Prometheus Service, Trial Edition and Pro Edition, were released for public preview on September 17, 2020.

## Pricing

Prometheus Service charges you based on the number of reported metrics. The metrics are classified into two types: basic metrics and custom metrics. You can use basic metrics for free but must pay for custom metrics.

Basic metrics are the monitoring metrics of [Container Service for Kubernetes \(ACK\)](https://www.alibabacloud.com/zh/product/kubernetes). For more information, see [Basic metrics]().

|Metric type|Trial Edition|Pro Edition|
|-----------|-------------|-----------|
|Basic metric|Free|Free|
|Custom metric|Daily free quota: 200 million|Not free|

## Trial Edition

When you activate the Trial Edition of Application Real-Time Monitoring Service \(ARMS\), the Trial Edition of Prometheus Service is activated at the same time. The trial period is valid until 00:00 on the 15th day after you activate ARMS. During the trial period, you can report up to 200 million custom metrics each day for free.

For more information about how to use ARMS Trial Edition, see [15-day free trial of ARMS](/intl.en-US/Billing/15-day free trial of ARMS.md).

**Note:**

-   When the number of metrics reported to the Trial Edition of Prometheus Service reaches 200 million in a day, Prometheus Service stops receiving more data on that day. If you want Prometheus Service to continue receiving data, upgrade Prometheus Service to the Pro Edition.
-   If Prometheus Service is not upgraded to the Pro Edition after the 15-day trial period, Prometheus Service stops receiving data.
-   After the 15-day trial period, Prometheus Service clears reported data.

## Pro Edition

To continue using Prometheus Service after the trial period, you must activate the Pro Edition.

**Note:**

-   The size of a reported metric cannot exceed 2 KB.
-   A reported metric is stored for up to 15 days. After that, the metric is cleared.

You are charged for custom metrics based on the number of daily reported metrics. Fees are cumulatively calculated in a stepwise decreasing manner. The following table describes pricing details for the China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), and China \(Shenzhen\) regions.

|Number of daily reported metrics \(million\)|Unit price \(USD/million\)|Daily cost \(USD\)|
|--------------------------------------------|--------------------------|------------------|
|0~50|0.118|0~5.9|
|50~150|0.096|5.9~15.5|
|150~300|0.081|15.5~27.65|
|300~600|0.067|27.65~47.75|
|600~1200|0.052|47.75~78.95|
|More than 1,200|0.037|More than 78.95|

The following table describes pricing details for the Singapore \(Singapore\) region.

|Number of daily reported metrics \(million\)|Unit price \(USD/million\)|Daily cost \(USD\)|
|--------------------------------------------|--------------------------|------------------|
|0~50|0.166|0~8.3|
|50~150|0.135|8.3~21.8|
|150~300|0.114|21.8~38.9|
|300~600|0.093|38.9~66.8|
|600~1200|0.072|66.8~110|
|More than 1,200|0.052|More than 110|

Assume that you activate Prometheus Service in the China \(Hangzhou\) region. If the average number of daily reported metrics is 300 million, which includes 200 million basic metrics and 100 million custom metrics, your monthly cost is calculated by using the following formula:

Cost = \[50 × 0.118 + \(100 - 50\) × 0.096\] × 30 = 321 \(USD\)

To view the total consumption of the previous day, perform the following operations: Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). On the Prometheus Monitoring page, click **Resource Consumption** in the upper-right corner.

**Related topics**  


[Basic metrics]()

