# Terms

This topic describes basic concepts before using tracing analysis, including the role of the distributed tracing system, what a call chain is, the OpenTracing data model that tracing links depend on, and how data is reported to the tracing system.

## Why is a distributed tracing system needed?

In order to cope with various complex business, development engineers began to adopt Agile development, continuous integration and other development methods. The system architecture has evolved from a stand-alone software system to a microservices model. Microservices are built on different sets of software, which may be developed by different teams, implemented in different programming languages, or released on multiple servers. Therefore, if a service error occurs, it may cause service exceptions in dozens of applications.

The distributed tracing system can record request information, such as the execution process and time consumption of a remote method call. It is an important tool for troubleshooting system problems and system performance.

## What is a Trace?

Broadly speaking, a trace of call represents the execution process of a transaction or process in a \(distributed\) system. In the OpenTracing standard, a call chain is a Directed Acyclic Graph \(Directed Acyclic Graph\) composed of multiple spans. Each Span represents a named and timed continuous execution segment in the call chain.

The following example shows a distributed call. When a client initiates a request, the request first goes to the Server Load Balancer, passes through the authentication service, billing service, and finally the resource, and finally returns the result.

![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/xtrace_dg_distributed_call.png "Example of a distributed call")

After the system collects and stores the data, the distributed tracing system can be used to generate a timing diagram that contains a timeline.

![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/arms/xtrace_dg_trace_graph.png "Link diagram containing the timeline")

## Data Model

**Overall concept**

In OpenTracing, a Trace is implicitly defined by the Span in this Trace. A trace can be considered as a directed acyclic graph \(DAG\) that consists of multiple spans. The relationship between spans is named References. The call chain in the following example consists of eight spans.

```

     Causal relationship between spans in A single Trace [Span A] ← ←(The root Span) | + ------ + ------ + | | [span B] [Span C] ← ←(Span C is A child node of Span A, ChildOf) | [Span D] + --- + ------- + | | [Span E] [Span F] |result> [Span G] |result> [Span H] // Trigger function (Span G is called after Span F, FollowsFrom) 
   
```

In some cases, a timing diagram based on a timeline can be used to better display the call chain.

```

     time relationship between spans in A single Trace -- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |-> time [Span A&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip; ..&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip; ..] [Span C&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip;&hellip; ..] [Span E&hellip;&hellip;&hellip;&hellip;] [Span F.] [span G ·] [Span H ·] 
   
```

**Link**

You can call this operation to create tracers \( startSpan\), Extract \( Extract\), and Inject \(passthrough\). It has the following capabilities:

-   Create a new Span or set the Span property

    ```
    
           /**Create and start a span. On the page that appears, specify the name of the operation and options. **For example,** create a Span: **sp := tracer. Without parentSpan. StartSpan(" GetFeed ") ** create a Span with parentSpan * sp := tracer.StartSpan("GetFeed",opentracing.ChildOf(parentSpan.Context())) example */ StartSpan(operationName string, opts ...StartSpanOption) Span 
         
    ```

    Each Span contains the following objects:

    -   Operation name: Operation name \(also known as Span name\).
    -   Start timestamp: The Start time of the day period.
    -   Finish timestamp: indicates the end time.
    -   Span tag: a set of Span tags. It is composed of a set of key-value pairs. In a key-value pair, the key must be a String and the value can be a String, Boolean, or numeric value.
    -   Span log: A Collection of Span logs. Each Log operation contains one key-value pair and one timestamp. In a key-value pair, the key must be a String and the value can be of any type.
    -   SpanContext: The pan context object. Each SpanContext contains the following states:
        -   To implement any OpenTracing service, it must rely on a unique Span to transmit the status of the current call chain across process boundaries \(for example, the Trace and Span ids\).
        -   Baggage Items are the data accompanying a Trace and a collection of key-value pairs. They are stored in a Trace and must be transmitted across process boundaries.
    -   References \(relationship between spans\): Zero or multiple related spans. Spans establish the relationship based on the SpanContext.
-   Pass-through data

    Passthrough data is divided into two steps:

    1.  Parses the SpanContext object from the request.

        ```
        
                 // Inject() takes the `sm` SpanContext instance and injects it for // propagation within `carrier`. The actual type of `carrier` depends on // the value of `format`. /**Parse the SpanContext (including traceId, spanId, and bagged) from the Carrier based on the format parameter. **Example:** carrier := opentracing.HTTPHeadersCarrier(httpReq.Header) // * clientContext, err := tracer.Extract(opentracing.HTTPHeaders, carrier) // */ Extract(format interface parameter parameter, carrier interface{}) (spanccontext, error) 
               
        ```

    2.  Inject SpanContext to the request.

        ```
        
                 /**Inject *** inject traceId,spanId, and Baggage in SpanContext to the request (Carrier) according to the format parameter. **e.g** carrier := opentracing.HTTPHeadersCarrier(httpReq.Header) then * err := tracer.Inject(span.Context(), opentracing.HTTPHeaders, carrier) producer */ Inject(sm SpanContext, format interface response parameter, carrier interface{}) error 
               
        ```


