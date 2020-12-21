# Commercial release announcement regarding ARMS Prometheus Monitoring

Prometheus Monitoring of Application Real-Time Monitoring Service \(ARMS\) became commercially available on January 6, 2020. Two editions are available: Trial Edition and Pro Edition. For all beta users, we automatically activated the Trial Edition of ARMS Prometheus Monitoring on January 6, 2020.

## Pricing principle

ARMS Prometheus Monitoring will charge you based on the number of reported metrics. There are two types of metrics: basic metrics and custom metrics. Basic metrics are free, and custom metrics are charged starting from January 6, 2020.

Basic metrics mainly are monitoring metrics related to [Container Service for Kubernetes](https://www.alibabacloud.com/zh/product/kubernetes).

|Metric type|Trial Edition|Pro Edition|
|-----------|-------------|-----------|
|Basic metric|Free|Free|
|Custom metric|Daily free quota: 200 million custom metrics|You will be charged|

## Trial Edition

When you activate ARMS, you can use the Trial Edition of ARMS Prometheus Monitoring for free. The trial period is valid until 00:00 on the 15th day after you activate ARMS. During the trial period, the daily free quota is 200 million custom metrics.

**Note:**

-   For Trial Edition users, ARMS stops receiving data after reporting 200 million custom metrics. To continue receiving data, you need to purchase the Pro Edition.
-   After the 15-day free trial, ARMS stops receiving data unless you purchase the Pro Edition.
-   Your data will be cleared on the 15th day after the trial period. For example, if the trial expires on February 1, your data will be cleared on February 16.

## Pro Edition

To continue using ARMS Prometheus Monitoring, you need to purchase the Pro Edition after the trial expires.

**Note:**

-   The size of a reported metric cannot exceed 2 KB.
-   Metric data is stored for up to 15 days. After that, the metric data will be cleared.

Custom metrics are charged based on the number of daily reported metrics. Charges are calculated cumulatively in a stepwise decreasing manner. The following table provides pricing details for the China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\) and China \(Shenzhen\) regions.

|Number of daily reported metrics \(million\)|Unit price \(USD/million\)|Daily cost \(USD\)|
|--------------------------------------------|--------------------------|------------------|
|0-50|0.118|0-5.9|
|50-150|0.096|5.9-15.5|
|150-300|0.081|15.5-27.65|
|300-600|0.067|27.65-47.75|
|600-1,200|0.052|47.75-78.95|
|More than 1,200|0.037|More than 78.95|

The following table provides pricing details for the Singapore region.

|Number of daily reported metrics \(million\)|Unit price \(USD/million\)|Daily cost \(USD\)|
|--------------------------------------------|--------------------------|------------------|
|0-50|0.166|0-8.3|
|50-150|0.135|8.3-21.8|
|150-300|0.114|21.8-38.9|
|300-600|0.093|38.9-66.8|
|600-1,200|0.072|66.8-110|
|More than 1,200|0.052|More than 110|

Take the China \(Hangzhou\) region as an example. Assume that the average number of daily reported metrics is 300 million, which includes 200 million basic metrics and 100 million custom metrics. You can estimate the monthly cost as follows:

Cost = \(50 × 0.118 + \(100 - 50\) × 0.096\) × 30 = 321 \(USD\)

Log on to the [ARMS console](https://arms-ap-southeast-1.console.aliyun.com/#/home). In the Prometheus Monitoring page, click **Resource Consumption** in the upper-right corner to view the total consumption of the previous day.

