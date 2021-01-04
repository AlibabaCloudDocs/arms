# Pricing adjustment

Tracing Analysis has updated its pricing model at 00:00 on October 11, 2020. After the update, the service is billed in a more cost-efficient and flexible way. You can continue to use the original billing model until your resource plan is used up. You can also update to the new billing model in the Tracing Analysis console.



## Price advantages

To compete with other self-managed open source products, Tracing Analysis has been continuously optimized for higher cost effectiveness. Compared with most mainstream open source application performance management \(APM\) systems that store data for only seven days, Tracing Analysis lacks flexibility by storing data for 30 days by default.

In the new pricing model, computing and storage are separately billed so that you can use this service in a better on-demand mode. In addition, you can adjust the storage duration of data in real time based on your business needs. This way, the cost can be reduced.

|Customer type|Number of nodes for a customer|Number of requests per day|Server configuration|Cost of open source products \(CNY/month\)|Cost of Tracing Analysis \(CNY/month\)|
|-------------|------------------------------|--------------------------|--------------------|------------------------------------------|--------------------------------------|
|Small-sized customer|80|20 million requests. Request complexity: 5 spans per request on average.|-   4 Elasticsearch servers. Server specifications: 4 CPUs, 16 GB memory, and 1 TB SSD.
-   4 Collector servers. Server specifications: 4 CPUs and 8 GB memory.

|5,836|764.8|
|Medium-sized customer|300|300 million requests. Request complexity: 7 spans per request on average.|-   8 Elasticsearch servers. Server specifications: 8 CPUs, 16 GB memory, and 6 TB SSD.
-   8 Collector servers. Server specifications: 4 CPUs and 8 GB memory.

|22,480|16,065|
|Large-sized customer|1,000|1 billion requests. Request complexity: 8 spans per request on average.|-   12 Elasticsearch servers. Server specifications: 16 CPUs, 64 GB memory, and 21 TB SSD.
-   16 Collector servers. Server specifications: 4 CPUs and 8 GB memory.

|65,088|64,800|
|Remarks|N/A|Based on the Apache documentation, each trace can report data that is 10 KB in size.|All statistical data is stored for 15 days and full detail data is stored for 7 days.|-|You are charged based on the total number of requests that are stored for your application. The total number of requests is equal to the number of requests per day multiplied by the duration. Open source agents are used. Components except for agents are maintained by Alibaba Cloud.|

## Comparison between the original and new pricing models

-   Original pricing model: You are charged based on the number of requests. All data is stored for 30 days.
-   New pricing model: The fixed 30-day price is no longer used. You are charged for computing and storage separately in the following ways:

    -   Computing fee for traces: CNY 0.9 per million request traces that are reported.
    -   Storage fee for traces: CNY 0.2 per million request traces that are stored.
    -   Storage fee for statistical metrics: CNY 0.01 per million metrics that are stored.
    **Note:**

    -   Computing fee for traces: The fee is calculated based on the number of request traces that are reported. The reported request traces are aggregated to generate statistical metrics of applications, APIs, and databases, such as the elapsed time, queries per second \(QPS\), and number of exceptions. You can configure the sample rate in the Tracing Analysis console to adjust the number of request traces that are reported.

        Example: When one million requests are reported per day, you are charged for CNY 0.9, which is calculated based on the following formula: 1 million × CNY 0.9/million = CNY 0.9.

    -   Storage fee for traces: The fee is calculated in the unit of one million request traces.

        Example: Assume that one million request traces are reported per day on average, and the traces are stored for 15 days. The total number of traces is 15 million, which is calculated based on the following formula: 15 days × 1 million/day = 15 million. In this case, the storage fee for the traces per day is CNY 3, which is calculated based on the following formula: 15 million × CNY 0.2/million = CNY 3.

    -   Storage fee for statistical metrics: The fee is calculated in the unit of one million metrics. Metrics are statistical data of applications, APIs, and databases, such as the request data, response time, and number of exceptions. One million requests generate about one million metrics.

        Example: Assume that one million metrics are generated per day on average, and the metrics are stored for 15 days. The total number of metrics is 15 million, which is calculated based on the following formula: 15 days × 1 million/day = 15 million. In this case, the storage fee for the metrics per day is CNY 0.15, which is calculated based on the following formula: 15 million × CNY 0.01/million = CNY 0.15.

    -   Request trace definition: All spans with the same trace ID in an Alibaba Cloud account are considered to belong to the same request. A request can contain up to 10 spans. For more information about spans, see [Terms](/intl.en-US/Overview/Terms.md). For each additional span, you are charged for one-tenth of the price for each request. The size of each span cannot exceed 2 KB. Excessive data of a span is discarded.
    -   Billing method:
        -   Tracing Analysis is billed daily. A bill for the previous day is generated at 00:00 every day.
        -   The computing fee for traces is calculated only for the number of request traces that are reported on a single day.
        -   The storage fee is calculated based on the storage capacity occupied by request traces or statistical metrics. The total storage capacity is calculated every day, and is affected by the storage duration. You can log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) and select an appropriate storage duration on the Cluster Configurations tab.

## Cases of comparison between the original and new pricing models

-   Original pricing model: All data is stored for 30 days. You are charged for CNY 5,300 per day for the 400 million requests.
-   New pricing model:
    -   Solution 1: stores both request traces and statistical metrics for 30 days.

        Computing fee for traces per day: 400 million/day × CNY 0.9/million = CNY 360/day.

        Storage fee for traces per day: 400 million/day × 30 days × CNY 0.2/million = CNY 2,400/day.

        Storage fee for statistical metrics per day: 400 million/day × 30 days × CNY 0.01/million = CNY 120/day. 400 million requests generate about 400 million metrics.

        Total: CNY 2,880 per day.

    -   Solution 2: stores request traces for 7 days and statistical metrics for 30 days.

        Computing fee for traces per day: 400 million/day × CNY 0.9/million = CNY 360/day.

        Storage fee for traces per day: 400 million/day × 7 days × CNY 0.2/million = CNY 560/day.

        Storage fee for statistical metrics per day: 400 million/day × 30 days × CNY 0.01/million = CNY 120/day. 400 million requests generate about 400 million metrics.

        Total: CNY 1,040 per day.


New pricing model: stores request traces for 7 days and statistical metrics for 30 days.

Computing fee for traces per day: 10 million/day × CNY 0.9/million = CNY 9/day.

Storage fee for traces per day: 10 million/day × 7 days × CNY 0.2/million = CNY 14/day.

Storage fee for statistical metrics per day: 10 million/day × 30 days × CNY 0.01/million = CNY 3/day. 10 million requests generate about 10 million metrics.

Total: CNY 26 per day.

## Update to the new pricing model

-   If you have not purchased a resource plan, you can log on to the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) and click **Save** on the Cluster Configurations tab to update to the new pricing model. On the next day, you can log on to the Tracing Analysis console and click the button in the upper-right corner of the Overview page. Then, you can view the fees billed in the new pricing model on the usage details page of resources.
-   If you have purchased a resource plan, you must [submit a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to apply for a refund for the resource plan. Then, you can update to the new pricing model.
-   The billing of all customers will be automatically updated to the new pricing model at 00:00 on April 1, 2021.

