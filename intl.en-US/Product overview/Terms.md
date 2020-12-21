# Terms

This topic lists the terms of Application Real-Time Monitoring Service \(ARMS\).

[B](#B) \| [C](#C) \| [J](#J) \| [S](#S) \| [Y](#Y) \| [Z](#Z)

## B

-   **Alert rule**

    An alert rule defines how to trigger alerts based on datasets and send alert notifications through a specific channel. The severity of an alert can be Warning, Error, or Critical.


[\[Back to the top\]](#top)

## C

-   **Collection rule**

    A collection rule defines how to collect data from data source instances in a custom monitoring job. You must define collection rules for custom monitoring jobs.


[\[Back to the top\]](#top)

## J

-   **Dashboard**

    A dashboard is a set of interactive monitoring data reports customized based on datasets in ARMS. The dashboard can display datasets by using different types of charts. The query time range of the dashboard is user-defined.


[\[Back to the top\]](#top)

## S

-   **Dataset**

    A dataset defines how to pre-aggregate and persistently store the logs that are collected in monitoring jobs. You can define a dataset directly or indirectly by using the dashboard and alert notification features.

-   **Dataset dimension**

    A dataset dimension is the key used for aggregation when a dataset is created. It is similar to the GroupBy column name in a database, or an attribute in multidimensional Online Analytical Processing \(OLAP\). A dataset performs aggregation operations on the real-time data based on the configured dimensions.

-   **Dataset metric**

    A dataset metric is a specific monitoring metric stored in a dataset, which is typically of the numerical type and similar to a value in multidimensional OLAP. ARMS metrics correspond to values of Count, Max, Sum, and Count Distinct after real-time computing.

-   **Data cleansing**

    Data cleansing is a process during which operations such as splitting and static join are performed on custom monitoring logs to convert them into standard key-value \(KV\) pairs.

-   **Data screening**

    Data screening is used to filter the data in datasets for dataset calculation. Data that do not meet criteria are filtered out from the dataset.

-   **Data source**

    A data source is the source of logs obtained by ARMS custom monitoring jobs, including Elastic Compute Service \(ECS\), Message Queue \(MQ\), and SDK data sources.


[\[Back to the top\]](#top)

## Y

-   **Mapping table**

    A custom static mapping table is used for mapping query results to business attribute fields. For example, you can map the province, city, and district names in query results to postal codes.


## Z

-   **Custom monitoring job**

    A custom monitoring job is a process in which ARMS captures, processes, and stores data, and then presents and exports the results. Custom monitoring jobs are divided into the following categories:


[\[Back to the top\]](#top)

## Links to other terms

-   [Terms of application monitoring](/intl.en-US/Application monitoring/Reference/Key statistical metrics.md)
-   [Terms of browser monitoring](/intl.en-US/Browser monitoring/Statistical metrics.md)

