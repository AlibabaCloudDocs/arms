# ARMS SDK

This topic describes how to use Application Real-Time Monitoring Service \(ARMS\) SDK to dynamically obtain TraceId and its properties in the service code.

## Prerequisites

-   An application monitoring task is created in the ARMS console, and the ARMS agent for application monitoring is installed and started in the Java program. For more information, see [Manually install the ARMS agent for a Java application](/intl.en-US/Application monitoring/Start monitoring Java applications/Manually install the ARMS agent for a Java application.md).
-   arms-sdk-1.7.3.jar is introduced to the program.

    ```
    <dependency>
        <groupId>com.alibaba.arms.apm</groupId>
        <artifactId>arms-sdk</artifactId>
        <version>1.7.3</version>
    </dependency>
    ```

    **Note:** If you cannot obtain the pom.xml file, download [arms-sdk-1.7.3.jar](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/arms-sdk-1.7.3.jar).


## Obtain TraceId and RpcId

You can run the following code to obtain TraceId and RpcId:

```
Span span = Tracer.builder().getSpan();
String traceId = span.getTraceId();
String rpcId = span.getRpcId();
```

## Pass through a custom tag baggage

To pass through a custom tag, you must add and obtain the tag from the service code. The following section describes the procedure:

1.  Add the baggage tag to the service code.

    ```
    Map<String, String> baggage = new HashMap<String, String>();
    baggage.put("key-01", "value-01");
    baggage.put("key-02", "value-02");
    baggage.put("key-03", "value-03");
    Span span = Tracer.builder().getSpan();
    span.withBaggage(baggage);
    ```

2.  Obtain the baggage tag from the service code.

    ```
    Span span = Tracer.builder().getSpan();
    Map<String, String> baggage = span.baggageItems();
    ```


## Set a custom tag tag for a span

A custom tag for a span applies to only the current span and is not passed to other spans. You must add and obtain the tag from the service code. The following section describes the procedure:

1.  Add a custom tag tag for a span in the service code. Multiple tags can be added.

    ```
    Span span = Tracer.builder().getSpan();
    // Add a tag to the Span.
    span.setTag("tag-key1", "tag-value1");
    span.setTag("tag-key2", "tag-value2");
    ```

2.  Obtain the tag from the service code.

    ```
    Span span = Tracer.builder().getSpan();
    // Inspect the Span's tags.
    Map<String, String> tags = span.tags();
    ```


## Query traces based on custom tags baggage and tag

The span tags baggage and tag can be used to query traces by tag.

-   Items on a baggage can be passed to the downstream and are generally used to color business data. We recommend that you do not set a large number of tag items.
-   Items on a tag apply to only the current span. You can set multiple items.

1.  Log on to the[ARMS console](https://arms-intl.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Application Monitoring** \> **Invocation Trace Query** and select a region in the top navigation bar.
3.  On the Invocation Trace Query page, select a **Parameter Name**, specify the custom tag in the **Parameter Value** field, and click **Query**.
4.  In the **Invocation Trace Query** list, click the **TraceID** of the destination trace.
5.  On the Invocation Trace page, move the pointer over **Service Name**. The information of tags that belong to the current span is displayed. baggage items are automatically added to tags of each span.

