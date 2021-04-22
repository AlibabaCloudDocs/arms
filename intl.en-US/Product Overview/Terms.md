# Terms

This topic lists the terms of Application Real-Time Monitoring Service \(ARMS\).

[B](#B) \| [C](#C) \| [J](#J) \| [S](#S) \| [Y](#Y) \| [Z](#Z)

## B

-   **alert rule**

    An alert rule defines how to trigger alerts based on datasets and send alert notifications through a specific channel. The severity of an alert can be Warning, Error, or Critical.


[\[Back to Top\]](#top)

## C

-   **collection rule**

    A collection rule defines how to collect data from data source instances in a custom monitoring job. You must define collection rules for custom monitoring jobs.


[\[Back to Top\]](#top)

## J

-   **dashboard**

    A dashboard is a set of interactive monitoring data reports that are customized based on datasets in ARMS. The dashboard can display datasets by using different types of charts. The query time range of the dashboard is user-defined.


[\[Back to Top\]](#top)

## S

-   **dataset**

    A dataset defines how to pre-aggregate and persistently store the logs that are collected in monitoring jobs. You can directly define a dataset, or indirectly define a dataset by using the dashboard and alert notification features.

-   **dataset dimension**

    A dataset dimension is the key used for aggregation when a dataset is created. It is similar to the GroupBy column name in a database, or an attribute in multi-dimensional online analytical processing \(OLAP\). A dataset performs aggregate operations on the real-time data based on the configured dimensions.

-   **dataset metric**

    A dataset metric is a specific monitoring metric stored in a dataset, which is typically of the NUMERIC type and similar to a value in multi-dimensional OLAP. ARMS metrics correspond to the values of Count, Max, Sum, and Count Distinct after real-time computing.

-   **data cleansing**

    Data cleansing is a process during which operations such as splitting and static join are performed on custom monitoring logs to convert them into standard key-value \(KV\) pairs.

-   **data screening**

    Data screening is used to filter the data in datasets for dataset calculation. Data that do not meet specific criteria is filtered out of the dataset.

-   **data source**

    A data source is the source of logs that are obtained by ARMS custom monitoring jobs, such as Elastic Compute Service \(ECS\), Message Queue \(MQ\), and SDK data sources.


[\[Back to Top\]](#top)

## Y

-   **mapping table**

    A mapping table is a custom static table that is used to map query results to business attribute fields. For example, you can map the province, city, and district names in query results to postal codes.


[\[Back to Top\]](#top)

## Z

-   **custom monitoring job**

    A custom monitoring job is a process in which ARMS captures, processes, and stores data, and then presents and exports the results. Custom monitoring jobs can be classified into the following types:


[\[Back to Top\]](#top)

## Links to other terms

-   [Terms of Application Monitoring](/intl.en-US/Application Monitoring/References/Key statistical metrics.md)
-   [Terms of Browser Monitoring](/intl.en-US/Browser Monitoring/Statistical metrics.md)

