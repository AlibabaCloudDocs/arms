# Billing adjustments

Tracing Analysis conducted at 00:00 on October 11, 202020, China, made a new upgrade to the pricing model, and was able to provide services in a more convenient and flexible way. You can use the original billing method until the resource package is consumed or upgrade to the new version on the console.



## Price advantage

As an open-source user-created product, link Tracing Analysis is always more cost-effective. However, most open-source application performance management \(APM\) instances only store 7 days of data. In contrast, the default storage duration of 30 days is inflexible enough.

Storage duration can be adjusted in real time to help you better use data on demand and control costs.

|Customer Type|Customer nodes|Requests per day|Machine configuration|Open-source cost \(RMB /month\)|Link Tracking \(RMB /month\)|
|-------------|--------------|----------------|---------------------|-------------------------------|----------------------------|
|Small customer|80|20 million requests \(request complexity: an average of 5 spans\)|-   Four Elasticsearch\(4 CPUs +16 GB of memory +1 TB SSD\)
-   Four collectors \(4CPU +8 GB memory\)

|5836|764.8|
|Medium customers|300|0.3 billion requests \(request complexity: an average of 7 spans\)|-   Eight Elasticsearch\(8CPU +16 GB memory +6 TB SSD hard disk\)
-   Eight Collectors \(4CPU +8 GB memory\)

|22480|16065|
|Large customer|1000|1 billion requests \(complex read requests: an average of 8 spans\)|-   12 Elasticsearch\(16CPU +64 GB memory +21 TB SSD hard disk\)
-   Sixteen collectors \(4CPU +8 GB memory\)

|65088|64800|
|Remarks|N/A|Based on Apache official, write 10 KB into a Trace.|All data is stored for 15 days based on the unified statistical data, and all detailed data is stored for seven days.|-|You are billed for the total number of requests stored by the application \(number of requests per day \* duration\). Open source probes are used. Other components are maintained by Alibaba Cloud.|

## Comparison of old and new selling price models

-   Old version: charged based on the number of requests, and all data is stored for 30 days.
-   In the new version, the original fixed price for 30 days is divided into the computing fee and the storage fee. The billing details are as follows:

    -   Link computing fee: USD 0.9 for each million reported request link.
    -   Link storage fee: RMB 0.2 per million request links stored.
    -   Storage fee for statistical metrics: USD 0.01 for each million storage metric.
    **Note:**

    -   Link computing fees: based on the number of channels for reporting requests, these indicators are aggregated to generate statistics for the requests \(such as the time consumption, QPS, and exceptions of applications, interfaces, and databases\). You can configure the sample rate in the console to adjust the number of reported events.

        For example, 1 million requests are reported every day. One million requests are reported per day. \* 0.9=0.9 yuan.

    -   Link storage fee: the cost of storing 1 million request links.

        Example: 1 million trace requests are reported every day. Assume that the total trace storage duration is 15 days and the total trace traffic is 15 million \(days\) × 1\(1 million\)=15 million Traces. Then, the total trace storage fee per day is 15 \(million\) × 0.2 \(unit price\)=3 RMB.

    -   Storage fee for statistical metrics: fees for storing 1 million metrics. Metrics are statistical data, such as request data, response time, and exception count of applications, interfaces, and databases. 1 million indicators will roughly produce 1 million indicators.

        Example: 1 million metrics are generated per day. Assume that the storage duration is 15 days and the total number of metrics is 15 days × 1 \(million metrics\)=15 million. The storage fee per day is 15 \(million\) × 0.01=0.15 RMB. 0.15 yuan is needed every day.

    -   Request trace: all the motion tracks with the same TraceID under an account are considered as one request. A request can contain up to 10 spans. For more information about the concept of Span, see the [Terms](/intl.en-US/Overview/Terms.md). A request of more than 10 spans is billed according to the number of spans contained in a request. Each Span cannot exceed 2kB, and the excess portion is discarded.
    -   Billing method:
        -   Tracing analysis is performed on a daily basis. Fees are charged at 00:00 every day for the day before that.
        -   Link calculation fees are only calculated for the traffic of the current day.
        -   Table store and quota storage are calculated based on the storage usage. The total storage usage is counted every day, which is related to the storage days. In the , [Tracing Analysis console](https://tracing-sg.console.aliyun.com/) On the cluster configuration page, adjust the storage duration.

## A comparison case of old and new price models

-   Original solution: All data was stored for 30 days, and 400 million requests were charged 5300 yuan per day.
-   New solution:
    -   Solution 1: Store link data and statistical indicator data for 30 days.

        Link fee calculated per day: 400\(400 million requests\) × 0.9 \(million unit price\)=360 yuan per day

        Storage fee per day: 400\(400 million requests\) × 30 \(days\) × 0.2 \(unit price of millions of requests\)=2,400 RMB /day

        Metric storage fee: 400\(400 million requests generate about 400 million metrics\) × 30 \(days\) × 0.01 \(unit price\)=CNY 120 /day

        Total: 2880 yuan /day

    -   Solution 2: link data is stored for 7 days and statistical metrics are stored for 30 days.

        Link fee calculated per day: 400\(400 million requests\) × 0.9 \(million unit price\)=360 yuan per day

        Storage fee per day: 400\(400 million requests\) × 7 \(days\) × 0.2 \(unit price of millions of requests\)=USD 560 per day

        Metric storage fee: 400\(400 million requests generate about 400 million metrics\) × 30 \(days\) × 0.01 \(unit price\)=CNY 120 /day

        Total: 1040 yuan /day


New solution: link data is stored for 7 days, and statistical metrics are stored for 30 days.

Link fee calculated per day: 10\(10 million requests\) × 0.9 \(million computation fees\)=9 CNY /day

Storage fees per day: 10 million requests × 7 \(days\) × 0.2 \(unit price of millions of requests\)=CNY 14 per day

Metric storage fee: Query rate: Daily total fees of 10\(10 million requests generates 10 million metrics\) × 30 \(days\) × 0.01 \(unit price of millions of metrics\)=CNY 3 /day

Total: 26 yuan /day

## Billing by upgrading the new version

-   If you have not purchased resource package, log on to the . In the [Tracing Analysis console](https://tracing-sg.console.aliyun.com/), click cluster configuration on the **save** page to complete the upgrade. You can estimate the expected fee of the new version by viewing the resource usage in the upper-right corner of the homepage of the console on the next day.
-   Customers who have purchased a resource package need to refund the resource package \(submit a [ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to apply for resource package refund\) before they can upgrade.
-   All customers will automatically upgrade to the new billing model after 00:00 on April 01, 2021.

