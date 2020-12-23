# How do I customize data queries?

The data that is collected by Tracing Analysis is stored in Log Service. You can write SQL statements to query data based on data formats.

By default, the data that is collected by Tracing Analysis is stored in Log Service. Format of a Log Service project:

```
proj-xtrade-***-{regionId}
```

Example:

```
proj-xtrace-6dcbb77ef4ba6ef5466b5debf9e2f951-cn-beijing
```

## Query spans of a trace

Format of a Logstore:

```
logstore-xtrace-{userId}-{regionId}
```

Example:

```
logstore-xtrace-123456789-cn-beijing
```

|Field|Description|
|-----|-----------|
|traceId|The ID of the trace. Example: fic891bb8f81e7fb.|
|timestamp|The time when the span is generated. Unit: microseconds. Example: 1607410144095000.|
|rpc|The name of the span or operator. Example: /health.|
|serviceName|The name of the microservice or application in which the trace resides. Example: order.|
|serverIp|The IP address of the server in which the span resides. Example: 127.0.0.1.|
|elapsed|The period that the span uses to process the request. Unit: microseconds. For example, the value 1000 indicates 1 millisecond.|
|spanId|The ID of the span. Example: fic891bb8f81e7fc.|
|parentSpanId|The ID of the parent span. Example: fic891bb8f81e7fb.|
|anno|The tag of the span. Example: lb=prod&.|

Examples of scenarios:

-   Query the requests that take more than 1 second to process

    ```
    elapsed > 1000 | select distinct traceId
    ```

-   Query the requests that take more than 1 second to process and go through the server with the IP address 172.16.0.0

    ```
    * and serverIp = "172.16.0.0" and elapsed > 1000 | select distinct traceId
    ```


## Query metrics of a trace

Format of a Logstore:

```
logstore-xtrace-{userId}-stat-{regionId}
```

Example:

```
logstore-xtrace-123456789-stat-cn-beijing
```

|Field|Description|
|-----|-----------|
|serviceName|The name of the microservice or application in which the trace resides. Example: order.|
|rpc|The name of the span or operator. Example: /health.|
|elapsed|The total number of milliseconds that the span uses to process requests at the specified time point. For example, the value 10 indicates 10 milliseconds.|
|avg\_elapsed|The average number of milliseconds that the span uses to process each request at the specified time point. For example, the value 10 indicates 10 milliseconds.|
|count|The total number of data records at the specified time point. For example: 10.|
|timestamp|The time point to query. Unit: milliseconds. Example: 1607410144000.|

Examples of scenarios:

-   Query the average number of requests that is processed by the /api1 span

    ```
    rpc: "/api1" |select sum(count) qps timestamp GROUP by timestamp
    ```

-   Query the average number of milliseconds that the /api1 span uses to process each request

    ```
    rpc: "/api1" |select sum(elapsed) /sum(count) rt, timestamp GROUP by timestamp
    ```


