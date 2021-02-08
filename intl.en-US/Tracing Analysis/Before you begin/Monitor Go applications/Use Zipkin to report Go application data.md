# Use Zipkin to report Go application data

Zipkin is a distributed tracing system. It is an open source system that is developed by Twitter to trace real-time data. Zipkin is used to aggregate real-time monitoring data that is collected from multiple heterogeneous systems. In Tracing Analysis, you can use Zipkin to report Go application data.



## Add instrumentation to the code

To use Zipkin to report Go application data to the Tracing Analysis console, you must first add instrumentation to the code.

1.  Add dependencies.

    ```
    [[constraint]]
      name = "github.com/openzipkin/zipkin-go"
      version = "0.1.1"
    
    [[constraint]]
      name = "github.com/gorilla/mux"
      version = "1.6.2"
    ```

2.  Create a Tracer object. The Tracer object can be used to create spans that record the time of distributed operations. The Tracer object contains information such as the endpoint for data reporting, IP address of the on-premises server, and sampling rate. You can adjust the sampling rate to reduce the overheads that are generated in data reporting.

    ```
    func getTracer(serviceName string, ip string) *zipkin.Tracer {
      // create a reporter to be used by the tracer
      reporter := httpreporter.NewReporter("http://tracing-analysis-dc-hz.aliyuncs.com/adapt_aokcdqnxyz@123456ff_abcdef123@abcdef123/api/v2/spans")
      // set-up the local endpoint for our service
      endpoint, _ := zipkin.NewEndpoint(serviceName, ip)
      // set-up our sampling strategy
      sampler := zipkin.NewModuloSampler(1)
      // initialize the tracer
      tracer, _ := zipkin.NewTracer(
        reporter,
        zipkin.WithLocalEndpoint(endpoint),
        zipkin.WithSampler(sampler),
      )
      return tracer;
    }
    ```

3.  Record the request data.

    ```
    // tracer can now be used to create spans.
    span := tracer.StartSpan("some_operation")
    // ... do some work ...
    span.Finish()
    // Output:
    ```

    **Note:**

    You can run the preceding code to create a root span that records the root operation of a request. If you need to record the previous and next operations of a request, inject a context. Sample code:

    ```
    childSpan := tracer.StartSpan("some_operation2", zipkin.Parent(span.Context()))
        // ... do some work ...
    childSpan.Finish()
    ```

4.  Add custom tags to a span for quick troubleshooting. For example, you can add a custom tag to check whether an error occurs or to record the return value of a request.

    ```
    childSpan.Tag("http.status_code", statusCode)
    ```

5.  In a distributed system, remote procedure call \(RPC\) requests are sent along with trace data. Trace data contains the values of the TraceId, ParentSpanId, SpanId, and Sampled parameters. You can call the Extract or Inject method to pass data in HTTP request headers. The following figure shows the overall process.

    ```
       Client Span                                                Server Span
    ┌──────────────────┐                                       ┌──────────────────┐
    │                  │                                       │                  │
    │   TraceContext   │           Http Request Headers        │   TraceContext   │
    │ ┌──────────────┐ │          ┌───────────────────┐        │ ┌──────────────┐ │
    │ │ TraceId      │ │          │ X-B3-TraceId      │        │ │ TraceId      │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ ParentSpanId │ │ Inject   │ X-B3-ParentSpanId │Extract │ │ ParentSpanId │ │
    │ │              ├─┼─────────>│                   ├────────┼>│              │ │
    │ │ SpanId       │ │          │ X-B3-SpanId       │        │ │ SpanId       │ │
    │ │              │ │          │                   │        │ │              │ │
    │ │ Sampled      │ │          │ X-B3-Sampled      │        │ │ Sampled      │ │
    │ └──────────────┘ │          └───────────────────┘        │ └──────────────┘ │
    │                  │                                       │                  │
    └──────────────────┘                                       └──────────────────┘
    ```

    **Note:** Zipkin allows you to pass a context over the HTTP protocol or by using the gRPC framework.

    1.  Call the Inject method on the client to inject the context information.

        ```
        req, _ := http.NewRequest("GET", "/", nil)
        // configure a function that injects a trace context into a reques
        injector := b3.InjectHTTP(req)
        injector(sp.Context())
        ```

    2.  Call the Extract method on the server to extract the context information.

        ```
        req, _ := http.NewRequest("GET", "/", nil)
                b3.InjectHTTP(req)(sp.Context())
        
                b.ResetTimer()
                _ = b3.ExtractHTTP(copyRequest(req))
        ```


## Quick start

The following example shows you how to use Zipkin to report Go application data.

1.  Download the [Demo](https://arms-apm.oss-cn-hangzhou.aliyuncs.com/demo/zipkinTracingGoTest.zip) file.

2.  Change the endpoint for data reporting in the utils.go file.

    **Note:** Please`<endpoint>`Replace with the trace consoleOverviewThe corresponding clients and access points in the corresponding regions are displayed on the page. For more information about how to obtain access point information, see [Obtain access point information](#tab2).

3.  Install dependencies.

    ```
    dep ensure
    ```

4.  Run the test program.

    ```
    go run main.go
    ```

5.  View the reported data in the [Tracing Analysis console](https://tracing-analysis.console.aliyun.com/).


## FAQ

Q: Why is no data reported after I follow the steps in Quick start?

A: You can check the message that is returned when the program is running. You can also check whether the endpoint is valid. For example, if the `failed the request with status code 403` message is returned, you have specified an invalid username or password.

[Zipkin official website](https://zipkin.io/)

[Zipkin source code for Go](https://github.com/openzipkin/zipkin-go)

