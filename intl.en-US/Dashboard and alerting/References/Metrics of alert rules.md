# Metrics of alert rules

Each alert metric belongs to a specific type. Each type has one or more dimensions. This topic describes the alert rule metrics for Application Real-Time Monitoring \(ARMS\) application monitoring and browser monitoring.

## Background

Call errors differ from abnormal calls.

-   A call error is identified when the returned status code for an entire external call is greater than 400.
-   An abnormal call is a call during which an error is thrown due to an exception.

## Metrics of application monitoring alert rules

|Type|Dimension|Metric|
|----|---------|------|
|**Invocation\_Statistic**|**Interface\_Name**|**Invocation\_RT\_ms**: indicates the response time of calls to the application entry point \(including both HTTP and Dubbo calls\), database, and internal system. Unit: millisecond. You can use this metric to check for slow requests and determine whether any application exception occurs. **Note:** Compared with the response time metric displayed on pages, this metric also covers database calls and system internal calls. |
|**Invocation\_Count**: indicates the number of calls to the application entry point \(including both HTTP and Dubbo calls\), database, and internal system. You can use this metric to analyze the number of calls of an application, to determine the traffic volume and whether any exception occurs in the application. **Note:** Compared with the number of calls displayed on pages, this metric also covers database calls and system internal calls. |
|**Invocation\_ErrorCount**: indicates the number of errors in calls to the application entry point \(including both HTTP and Dubbo calls\), database, and internal system. You can use this metric to determine whether application exceptions or application call errors occur. **Note:** Compared with the number of errors displayed on pages, this metric also covers database calls and system internal calls. |
|**Invocation\_Type**|**Invocation\_Type**|**App\_Inbound\_Invoke\_RT\_ms**: indicates the response time of calls to the application entry point, including both HTTP and Dubbo calls. Unit: millisecond. You can use this metric to check for exceptions over the entire service trace.|
|**App\_Inbound\_Invoke\_Request**: indicates the number of calls to the application entry point, including both HTTP and Dubbo calls. You can use this metric to analyze the number of access requests over the entire service trace, to determine the traffic volume and whether any exception occurs in the application.|
|**App\_Inbound\_Exception\_Rate**: indicates the error rate of calls to the application entry point, including both HTTP and Dubbo calls. You can use this metric to check for errors over an entire service trace. For external services, you can determine the number of errors that occur when users failed to access the system.|
|**App\_Outbound\_Invoke\_RT\_ms**: indicates the response time of downstream dependent service calls over the trace, such as inter-HTTP service calls and database calls. Unit: millisecond. You can use this metric to check for slow access to downstream systems, and determine whether any exception occurs in the application.|
|**App\_Outbound\_Invoke\_Request**: indicates the number of downstream dependent service calls over the trace, such as inter-HTTP service calls and database calls. You can use this metric to determine whether any exception occurs over the trace.|
|**App\_Outbound\_Exception\_Rate**: indicates the error rate of downstream dependent service calls over the trace, such as inter-HTTP service calls and database calls. You can use this metric to check for errors in downstream application calls, and determine whether exceptions occur over the entire trace.|
|**Database\_Metric**|**Database\_Name**|**DB\_RT\_ms**: indicates the response time for the application to call a database. Unit: millisecond. You can use this metric to check for slow database access from the application, and determine whether exceptions occur when the application calls the database or whether any exception exists in the database environment.|
|**DB\_Count**: indicates the number of database calls initiated by an application. You can use this metric to determine whether the application causes excessive pressure on the database and whether application exceptions occur.|
|**DB\_ErrorCount**: indicates the number of errors in database calls initiated by the application. You can use this metric to determine whether the application exception is caused by a database, and whether exceptions occur in the database or the database environment.|
|**JVM\_Monitoring**|**IP**|**JVM\_GcPsMarkSweepCount**: indicates the number of JVM tag cleanup events. This metric is not frequently used in alerts.|
|**JVM\_Non\_Heap\_Used\_byte**: indicates the JVM non-heap memory utilization. You can use this metric to determine whether an application occupies too much non-heap memory in scenarios where non-heap memory is used. You can also use this metric to determine whether exceptions occur in the application.|
|**JVM\_GcG1YoungGenCount**: indicates the number of Garbage-First Garbage Collector \(G1GC\) events in the JVM\_Young zone. This metric is not frequently used in alerts.|
|**JVM\_FullGC\_Count**: indicates the number of full garbage collection \(GC\) events. If the value is too large, you can determine that exceptions occur in the application.|
|**JVM\_FullGC\_Time\_ms**: indicates the time used for full GC. If the value is too large, you can determine that exceptions occur in the application.|
|**JVM\_Non\_Heap\_Init\_byte**: indicates the initial value of JVM non-heap memory. This metric is not frequently used in alerts.|
|**JVM\_Non\_Heap\_Committed\_byte**: indicates the committed JVM non-heap memory. This metric is not frequently used in alerts.|
|**JVM\_Young\_GC\_Instant\_Count**: indicates the number of JVM young GC events. If the value is too large, you can determine that exceptions occur in the application.|
|**JVM\_GcG1OldGenCount**: indicates the number of G1GC events in the JVM\_Old zone. This metric is not frequently used in alerts.|
|**JVM\_Non\_Heap\_Max\_byte**: indicates the maximum value of JVM non-heap memory. This metric is not frequently used in alerts.|
|**JVM\_Heap\_Total\_byte**: indicates the total capacity of JVM heap memory. If the value is too large, you can determine that exceptions occur in the system.|
|**JVM\_ThreadCount**: indicates the total number of JVM threads. You can use this metric to determine whether an application runs properly \(a value greater than 0 indicates that the application runs properly\), or whether a large number of threads exist, for example, in thread pool scenarios.|
|**JVM\_GcPsScavengeCount**: indicates the total number of JVM GC events. This metric is not frequently used in alerts.|
|**JVM\_Young\_GC\_Time\_Instant\_ms**: indicates the time used for JVM young GC. If the value is too large, you can determine that exceptions occur in the application.|
|**Host\_Monitoring**|**IP**|**Node\_User\_CPU\_percent**: indicates the CPU usage of a node. You can use this metric to determine whether an application occupies too much CPU resources. We recommend that the CPU usage of the application keep below 90%.|
|**Node\_Net\_In\_Errs**: indicates the number of error packets received by a node. You can use this metric to determine whether exceptions occur in the network where the node is located. This metric is not frequently used in alerts.|
|**Node\_Disk\_Free\_byte**: indicates the free disk space of a node. You can use this metric to determine whether a node disk is fully occupied. If a disk is fully occupied, exceptions may occur in the application.|
|**Node\_Net\_Out\_Errs**: indicates the number of error packets sent by a node. You can use this metric to determine whether exceptions occur in the network where the node is located. This metric is not frequently used in alerts.|
|**Node\_Load**: indicates the node load. You can use this metric to determine whether the current workload of a node is too high. For a node with N cores, keep the load below N. This metric is not frequently used in alerts.|
|**Node\_MEM\_Free\_Byte**: indicates the free memory of a node. You can use this metric to determine whether a node has sufficient memory. If the free memory of a node is low, exceptions such as out of memory \(OOM\) may occur.|
|**Exception\_Invocation**|**Interface\_Name**|**Exception\_Call\_Count**: indicates the number of abnormal calls of an application. An abnormal call is a call during which an error is thrown due to an exception. You can use this metric to determine whether a call stack throws errors and whether application call exceptions occur.|
|**Exception\_Call\_RT\_ms**: indicates the response time of abnormal calls of an application. An abnormal call is a call during which an error is thrown due to an exception. You can use this metric to determine the impact of errors thrown by the call stack on the call response time, and determine whether application call exceptions occur.|

## Metrics of browser monitoring alert rules

|Type|Dimension|Metric|
|----|---------|------|
|**Page\_API\_Metric**|**Page\_Name**, **API\_Name**|**Api\_Fail\_Time\_ms**: indicates the average request time when the API call of a page fails. You can use this metric to check whether the API request time of a page is normal.|
|**Api\_Request\_Count**: indicates the number of API calls of a specific page. You can use this metric to determine whether the API requests of a page are normal.|
|**Api\_Success\_Time\_ms**: indicates the average response time of successful API requests on a specific page. You can use this metric to check whether the response time of API requests on a page is normal.|
|**Api\_Success\_Rate**: indicates the ratio of successful API calls to total calls on a specific page. You can use this metric to check whether API calls on a page are normal.|
|**Custom\_Statistics\_Metric**|**Custom\_Statistics\_Key**|**Custom\_Statistics\_Sum**: indicates the summation field that is manually reported. In ARMS, this field is accumulated for custom tracing points.|
|**Custom\_Statistics\_Average**: indicates the average of the values that are manually reported. ARMS calculates the average value for custom tracing points.|
|**Page\_Metric**|**Page\_Name**|**DNS\_Lookup\_ms**: indicates the time consumed for page DNS connection. You can use this metric to determine whether the page access speed is normal.|
|**Custom\_first\_screen\_time\_ms**: indicates the first page display time that is manually reported. You can use this custom performance metric to determine whether the page access speed is normal.|
|**Custom\_first\_time\_to\_interact\_ms**: indicates the first time available for interaction that is manually reported. You can use this custom performance metric to determine whether the page access speed is normal.|
|**First paint time\_ms**: indicates the period from the time when a request is initiated to the time when the browser parses the bytes of the first batch of HTML documents. You can use this metric to determine whether the page access speed is normal.|
|**Resource\_Download\_ms**: indicates the time consumed for page resource loading. You can use this metric to determine whether the page access speed is normal.|
|**Custom\_t1-t10\_ms**: are custom performance fields that are manually reported as needed. You can customize these fields.|
|**Page\_View**: indicates how many times a page is viewed.|
|**Time\_to\_First\_Byte\_TTFB\_ms**: indicates the response time of network requests. You can use this metric to determine whether the page access speed is normal.|
|**DOM\_Ready\_ms**: indicates the HTML loading time, or the time elapsed before the document object model \(DOM\) is ready. You can use this metric to determine whether the page access speed is normal.|
|**DOM\_Parsing\_ms**: indicates the time consumed for parsing the DOM on the page. You can use this metric to determine whether the page access speed is normal.|
|**Page\_Satisfaction**: is calculated based on the first render time. Satisfactory cases refer to the cases with the first render time less than 2,000 ms. Tolerable cases refer to the cases with the first render time greater than 2,000 ms and less than 8,000 ms. Satisfaction = \(Satisfactory cases + Tolerable cases/2\)/Total sample cases|
|**JS\_Error\_Count**: indicates the number of JavaScript \(JS\) errors on a page.|
|**Time\_to\_First\_interaction\_ms**: indicates the time when the page becomes operable. You can use this metric to determine whether the page speed is normal.|
|**Content\_Download\_ms**: indicates the time consumed for transmitting page data. You can use this metric to determine whether the page access speed is normal.|
|**Fully\_Loaded\_Time\_ms**: indicates the time consumed for loading a page completely. Load = First render time + DOM parsing time + JS synchronization time + Resource loading time. You can use this metric to determine whether the page access speed is normal.|
|**TCP\_Connection\_ms**: indicates the time consumed for connecting to a page over TCP. You can use this metric to determine whether the page access speed is normal.|
|**First\_meaningful\_paint\_ms**: indicates the time when the main content of the page first appears on the screen. You can use this metric to determine whether the page access speed is normal.|
|**The\_uv\_of\_the\_fail\_api**: indicates the number of users who fail to call an API. You can use this metric to determine the impact of API call errors.|
|**JS\_Error\_Rate**: indicates the ratio of page views with JS errors to total page views. A higher JS error rate means a higher severity of JS errors.|
|**SSL\_Connection\_ms**: indicates the time consumed for establishing a Secure Sockets Layer \(SSL\) connection. You can use this metric to determine whether the page speed is normal.|
|**API\_Metric**|**API\_Name**|**API\_Success\_Rate**: indicates the ratio of successful API calls to total API calls. You can use this metric to determine whether API calls are normal.|
|**API\_Success\_Time\_ms**: indicates the average response time of all successful API calls. You can use this metric to determine whether the response time is normal.|
|**The\_uv\_of\_the\_fail\_api**: indicates the number of users who fail to call an API. You can use this metric to determine the impact of API call errors.|
|**API\_Fail\_Time\_ms**: indicates the average response time of all failed API calls. You can use this metric to determine whether the response time is normal.|
|**API\_Request\_Count**: indicates how many times an API is called. You can use this metric to determine whether API calls are normal.|

**Related topics**  


[Create an alert](/intl.en-US/Dashboard and alerting/Create an alert.md)

[Create common alert rules](/intl.en-US/Dashboard and alerting/Tutorials/Create common alert rules.md)

