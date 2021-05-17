# Billing adjustment

The billing model of Tracing Analysis was updated at 00:00 on October 11, 2020. The new billing model allows you to use Tracing Analysis in a more cost-efficient and flexible manner. You can use the original billing model until your resource plan is consumed. You are automatically charged based on the new billing model after you save the cluster configurations in the console.



## Benefits

Compared with other self-managed open source services, Tracing Analysis is continuously optimized for higher cost-effectiveness. Most open source application performance management \(APM\) systems store data for only seven days. However, Tracing Analysis stores data for 30 days by default. In this case, you cannot use Tracing Analysis in a flexible manner.

To meet your business requirements, Tracing Analysis provides the new billing model. You are charged based on the resources that are consumed for computing or storage. You can modify the retention period of your data. This reduces costs.

|Customer type|Number of nodes for a customer|Number of requests per day|Server configurations|Cost of open source services \(CNY/month\)|Cost of Tracing Analysis \(CNY/month\)|
|-------------|------------------------------|--------------------------|---------------------|------------------------------------------|--------------------------------------|
|Small-sized customer|80|20 million requests. Request complexity: 5 spans per request on average.|-   4 Elasticsearch servers. Server specifications: 4 CPUs, 16 GB of memory, and 1 TB SSD.
-   4 Collector servers. Server specifications: 4 CPUs and 8 GB of memory.

|5836|764.8|
|Medium-sized customer|300|300 million requests. Request complexity: 7 spans per request on average.|-   8 Elasticsearch servers. Server specifications: 8 CPUs, 16 GB of memory, and 6 TB SSD.
-   8 Collector servers. Server specifications: 4 CPUs and 8 GB of memory.

|22480|16065|
|Large-sized customer|1000|1 billion requests. Request complexity: 8 spans per request on average.|-   12 Elasticsearch servers. Server specifications: 16 CPUs, 64 GB of memory, and 21 TB SSD.
-   16 Collector servers. Server specifications: 4 CPUs and 8 GB of memory.

|65088|64800|

**Note:**

-   The number of nodes for a customer is the number of Elastic Compute Service \(ECS\) instances or the number of Docker containers.
-   The number of requests per day is calculated based on the Apache documentation. Each trace can report 10 KB of data.
-   Statistical data is stored for 15 days. Full detail data is stored for seven days.
-   You are charged based on the total number of requests that are stored for your application. Formula: Total number of requests = Number of requests per day × Data retention period. Open source agents are used. Other components are maintained by Alibaba Cloud.

## Comparison between the original and new billing models

-   Original billing model: You are charged based on the number of requests. All data is stored for 30 days.
-   New billing model: The fixed 30-day price is no longer used. You are charged for computing and storage based on the following details:

    -   Computing fee of traces: CNY 0.9 per million request traces that are reported.
    -   Storage fee of traces: CNY 0.2 per million request traces that are stored.
    -   Storage fee of statistical metrics: CNY 0.01 per million metrics that are stored.
    **Note:**

    -   Computing fee of traces: The fee is calculated based on the number of request traces that are reported. The reported request traces are aggregated to generate the statistical metrics of applications, APIs, and databases. The statistical metrics include the elapsed time, queries per second \(QPS\), and number of exceptions. You can set the sample rate in the Tracing Analysis console to modify the number of request traces that are reported.

        For example, one million requests are reported per day. In this case, the computing fee of the traces is CNY 0.9 \(1 million requests × CNY 0.9/million requests = CNY 0.9\).

    -   Storage fee of traces: The fee is calculated by one million request traces.

        For example, one million request traces are reported per day, and the traces are stored for 15 days. In this case, the total amount of stored traces is 15 million traces \(15 days × 1 million traces/day = 15 million traces\). The storage fee of the traces per day is CNY 3 \(15 million traces × CNY 0.2/million traces= CNY 3\).

    -   Storage fee of statistical metrics: The fee is calculated by one million metrics. Metrics, such as the request data, response time, and number of exceptions, are the statistical data of applications, APIs, and databases. One million request traces generate about one million metrics.

        For example, one million metrics are generated per day, and the metrics are stored for 15 days. In this case, the total amount of stored metrics are 15 million metrics \(15 days × 1 million metrics/day = 15 million metrics\). The storage fee of the metrics per day is CNY 0.15 \(15 million metrics × CNY 0.01/million metrics = CNY 0.15\).

    -   Request traces: All spans with the same trace ID in an Alibaba Cloud account are considered to be one request. A request can contain a maximum of 10 spans. For more information about spans, see [Terms](/intl.en-US/Product Introduction/Terms.md). For each additional span after the first, you are charged one-tenth of the price for each subsequent request. The size of each span cannot exceed 2 KB. The excess data of a span is discarded.
    -   Billing method:
        -   Fees are calculated on a daily basis in Tracing Analysis. A bill is generated at 00:00 every day for the previous day.
        -   The daily computing fee of traces is calculated based on the number of request traces that are reported within a day.
        -   The storage fee of request traces or statistical metrics is calculated based on the related storage capacity. The total storage capacity is calculated on a daily basis and based on the related data retention period. You can log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) and specify the retention period of request traces or statistical metrics on the Cluster Configurations tab.

## Cases of the new billing model

-   Solution 1: The request traces and statistical metrics are stored for 30 days.

    Computing fee of the traces per day = 400 million requests/day × CNY 0.9/million requests = CNY 360/day

    Storage fee of the traces per day = 400 million requests/day × 30 days × CNY 0.2/million requests = CNY 2,400/day

    In this example, 400 million requests generate 400 million metrics. Storage fee of the statistical metrics per day = 400 million metrics/day × 30 days × CNY 0.01/million metrics = CNY 120/day

    The total fee is CNY 2,880 per day.

-   Solution 2: The request traces are stored for seven days and the statistical metrics are stored for 30 days.

    Computing fee of the traces per day = 400 million requests/day × CNY 0.9/million requests = CNY 360/day

    Storage fee of the traces per day = 400 million requests/day × 7 days × CNY 0.2/million requests = CNY 560/day

    In this example, 400 million requests generate about 400 million metrics. Storage fee of the statistical metrics per day = 400 million metrics/day × 30 days × CNY 0.01/million metrics = CNY 120/day

    The total fee is CNY 1,040 per day.


Solution: The request traces are stored for seven days and the statistical metrics are stored for 30 days.

Computing fee of the traces per day = 10 million requests/day × CNY 0.9/million requests = CNY 9/day.

Storage fee of the traces per day = 10 million requests/day × 7 days × CNY 0.2/million requests = CNY 14/day.

In this example, 10 million requests generate about 10 million metrics. Storage fee of the statistical metrics per day =10 million metrics/day × 30 days × CNY 0.01/million metrics = CNY 3/day

The total fee is CNY 26 per day.

## Update the billing model

-   If you have not purchased a resource plan, you can log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) and click **Save** on the Cluster Configurations tab. The billing model is automatically updated. On the next day, you can log on to the Tracing Analysis console and click the button in the Resource status section of the Overview page. On the page that appears, you can calculate fees by using the new billing model based on the resource statuses.
-   If you have purchased a resource plan, you must [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to request a refund for the resource plan. Then, you can update the billing model.

