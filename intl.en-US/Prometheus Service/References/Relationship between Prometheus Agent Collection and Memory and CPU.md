# Relationship between Prometheus Agent Collection and Memory and CPU

This topic describes the relationship between Prometheus Agent collection and memory and CPU, and provides suggestions on resource usage.

## Agent Stress Test Report

|Single collection volume \(collection volume of a single agent\)|CPU|Memory|
|----------------------------------------------------------------|---|------|
|1,000,000|0.95 core|1.09483 GB|
|1,100,000|1.11 core|1.16045 GB|
|1,200,000|1.36 core|1.09452 GB|
|1,300,000|1.66 core|1.15971 GB|
|1.400,000|1.29 core|1.09465 GB|
|1,500,000|1.50 core|1.15977 GB|
|1,600,000|1.39 core|1.15971 GB|
|1,700,000|1.64 core|1.1599 GB|
|1,800,000|1.63 core|1.42331 GB|

A single acquisition can be carried out with PrometheusObtain the name of the Grafana dashboard page.

For example, for the following PromQL, the collection amount is shown in the following figure.

```

     sum (scrape_samples_scraped) by (_ARMS_AGENT_ID) 
   
```

![Grafana of Prometheus](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0905766261/p294607.png)

## Resource usage suggestions

According to the Agent stress test report, the 1 million collection requires about 1 GB of memory and 1-core CPU. However, for the collection process to run properly, we recommend that you allocate the usage of each 50% of CPU and memory to the Prometheus Agent to collect data.

The CPU and memory usage recommendations for different collection volumes are as follows:

-   The amount of 500 thousand collected. We recommend that you use 1 GB of memory and 1-core CPU.
-   The amount of 1 million collected. We recommend that you use 2 GB of memory and 2-core CPU.
-   The amount of 2 million collected. We recommend that you use 4 GB memory and 4-core CPU.
-   More parameter values can be set in the same manner.

Example: Assume that the collection volume reaches 1 million through the Grafana page. In this case, we recommend that you scale up the memory and CPU to 2 GB and 2 cores.

